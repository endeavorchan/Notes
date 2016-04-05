---
layout: post
title: Circulur Buffer
categories: [C++, Multi-thread]
tags: [Circulur Buffer]
description: Implementation of muti-thread circular queue
fullview: false
---

## C++ Thread Base Class



{% highlight c++ %}
namespace bl {
//const int QUEUESIZE = 20;
template<class T, int QUEUESIZE>
class CirQueue {
    T buf[QUEUESIZE];
    int head, tail;
    bool full, empty;
    pthread_mutex_t *_lock;
    pthread_cond_t *_notfull, *_notempty;
protected:
    void push(T in) {
        buf[tail] = in;
        tail++;
        if (tail == QUEUESIZE) {
            tail = 0;
        }
        if (tail == head) {
            full = true;
        } 
        empty = false;
        return;
    }

    T pop() {
        T out = buf[head];
        head++;
        if (head == QUEUESIZE) {
            head = 0;
        }
        if (head == tail)
            empty = true;
        full = false;
        return out;
    }
public:

    CirQueue() {
        head = 0;
        tail = 0;
        full = false;
        empty = true;
        _lock = new pthread_mutex_t;
        pthread_mutex_init(_lock, NULL);
        _notfull = new pthread_cond_t;
        pthread_cond_init(_notfull, NULL);
        _notempty = new pthread_cond_t;
        pthread_cond_init(_notempty, NULL);
    }

    virtual ~CirQueue() {
        pthread_mutex_destroy(_lock);
        delete _lock;
        pthread_cond_destroy(_notfull);
        delete _notfull;
        pthread_cond_destroy(_notempty);
        delete _notempty;
    }

    void produce(T &val) {
    	pthread_mutex_lock(_lock);
    	while (full) {
    		// queue full
    		pthread_cond_wait(_notfull, _lock);
    	}
    	push(val);
    	pthread_mutex_unlock(_lock);
    	pthread_cond_signal(_notempty);
    	return;
    }
    
    T consume() {
    	pthread_mutex_lock(_lock);
    	while (empty) {
    		// consumer: queue empty
    		pthread_cond_wait(_notempty, _lock);
    	}
    	
    	T ret = pop();
    	pthread_mutex_unlock(_lock);
    	phtread_cond_signal(_notfull);
    	return ret;
    }
    
};

} // namespace bl
    
{% endhighlight %}