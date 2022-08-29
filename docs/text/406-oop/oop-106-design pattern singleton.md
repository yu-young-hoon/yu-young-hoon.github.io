---
layout: default
title: oop design pattern singleton
parent: oop
nav_order: 406106
---

멀티스레드 개발에서 일관성을 보장해주는 방식
* 생성자 막기
* 소멸자 막기
* getter
* multithread

<source lang="cpp">
// C++
Foo* Foo::Instance() {
  if(pinstance == nullptr) {
    lock_guard<mutex> lock(m_);
    if(pinstance == nullptr) {
        pinstance = new Foo();
    }
  }
  return pinstance;
}
</source>
<source lang="cpp">
// JAVA
public static synchronized singleton getInstance () {
    if (instance == null)
        instance = new ThreadSafeInitalization();
    return instance;
}
</source>

<div class="mw-collapsible mw-collapsed">
접기
1. 주소 값을 이용한 방식
<source> 
class yh_singleton
{
public:
	static yh_singleton&amp; getInstanse(){
		static yh_singleton instance;
		return instance;
	};
	int num;
private:
	yh_singleton(){};
	yh_singleton(const yh_singleton&amp; other);
	yh_singleton&amp; operator=(yh_singleton&amp; cls);
	~yh_singleton(){};
};

yh_singleton&amp; yh= yh_singleton::getInstanse();
yh.num= 4;
</source>
2. 포인터를 이용한 방식
<source> 
class yh_singleton
{
public:
	static yh_singleton* getInstanse(){
		static yh_singleton instance;
		return &amp;instance;
	};
	int num;
private:
	yh_singleton(){};
	yh_singleton(const yh_singleton&amp; other);
	yh_singleton&amp; operator=(yh_singleton&amp; cls);
	~yh_singleton(){};
};

yh_singleton* yh= yh_singleton::getInstanse();
yh->;num= 4;
</source>
3. 템플릿 싱글톤
<source> 
template &lt;typename T&gt;
class yh_singleton
{
public:
	static T* getInstance()
	{
		if (instance == NULL)
			instance = new T;
		return instance;
	};

	static void destroyInstance()
	{
		if (instance)
		{
			delete instance;
			instance = NULL;
		}
	};
private:
static T* instance;
protected:
yh_singleton(const yh_singleton&amp; other);
yh_singleton&amp; operator=(yh_singleton&amp; cls);
yh_singleton();
virtual ~yh_singleton(){};
};
template &lt;typename T&gt;T * yh_singleton&lt;T&gt;::instance = NULL;

class ojectA : public yh_singleton&lt;ojectA&gt;
{
public:
ojectA();
~ojectA();

	int a;
};
</source>
</div>
