---
layout: post
title: C++ Thread Class
categories: [C++, Multi-thread]
tags: [C++ Thread Class]
description: This is a base thread class written in C++
fullview: false
---

## C++ Thread Base Class



{% highlight c++ %}

class Thread {
public:
	Thread() {}
	virtual ~Thread() {}
	
	virtual void run()=0;
	int start();
	int join();
protected:
	static void* thread_proc(void *para) {
		Thread *pthis = static_cast<Thread *>para;
		pthis->run();
	}
private:
	pthread_t pid;
};


int Thread::start() {
	if (pthread_create(&pid, NULL, Thread::thread_proc, (void*)this) != 0) {
		return -1;
	} else
		return 0;
}

int Thread::join() {
	if (pthread_join(&pid, NULL) != 0) {
		return -1;
	} else
		return 0;
}
    
{% endhighlight %}