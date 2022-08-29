---
layout: default
title: oop design pattern factory
parent: oop
nav_order: 406109
---

객체가 new를 통해서 인스턴스를 만드는 작업을 숨기고 느슨한 결합을 이용해서 불필요한 의존성을 없애는 패턴
<br /><br />
1. 팩토리 적용하기전의 상황 주문할때 피자종류선택과 피자 만드는 것을 한 장소에서 처리하기 때문에<br />
   피자 종류가 늘어난다면 피자종류를 선택하는 위치를 찾아서 중간에 코드를 끼워 넣어야함.
<source>
#include &lt;cstring&gt;
class yh_nonFactory
{
	public:
		Pizza* orderPizza(char* type){
			Pizza* pizza;
			if (strcmp("cheese",type)){
				pizza = new cheesePizza();
			}
			else if (strcmp("papalony",type)){
				pizza = new papalonyPizza();
			}
			pizza-&gt;prepare();
			pizza-&gt;bake();
			pizza-&gt;cut();
			pizza-&gt;box();
			return pizza;
		};
};

class Pizza{
public:
void prepare();
void bake();
void cut();
void box();

};

class cheesePizza : public Pizza{

};

class papalonyPizza : public Pizza{

};
</source>
<br />
2. 간단한 팩토리가 적용된 상황, 사실상 디자인 패턴은 아니지만 프로그래밍에 있어서<br />
자주 쓰이는 관용구 정도로 이해하면 좋음, 팩토리 패턴 아님.
<source>
#include &lt;cstring&gt;
class yh_store{
	yh_simpleFactory* factory;
public:
	yh_store(){
		factory = new yh_simpleFactory();
	};
	Pizza order(){
		Pizza* pizza;
		pizza = factory-&gt;createPizza("cheese");
		pizza-&gt;prepare();
		pizza-&gt;bake();
		pizza-&gt;cut();
		pizza-&gt;box();
	};
};
class yh_simpleFactory
{
public:
	Pizza* createPizza(char* type){
		Pizza* pizza;
		if (strcmp("cheese", type)){
			pizza = new cheesePizza();
		}
		else if (strcmp("papalony", type)){
			pizza = new papalonyPizza();
		}
	};
};

class Pizza{
public:
void prepare();
void bake();
void cut();
void box();

};
class cheesePizza : public Pizza{

};
class papalonyPizza : public Pizza{

};
</source>
<br />
3. Factory Method Pattern이 적용되서 factoryMethod를 상속받은 서브 클래스들이 피자 종류를 결정하는 방식<br />
- Factory Method 패턴과 Abstract Factory 패턴의 기본이 되는 패턴<br />

- Factory 패턴의 기본 모양에서 객체 생성을 Factory 클래스의 하위 클래스에서 처리하도록 하는 패턴<br />

- 생성하려는 객체의 클래스를 정확히 지정하지 않으면서 객체를 만드는 또 다른 메소드를 정의하여 처리<br />
<source>
class yh_factoryMethod
{
public:
	Pizza order(){
		Pizza* pizza;
		pizza = createPizza("cheese");
		pizza-&gt;prepare();
		pizza-&gt;bake();
		pizza-&gt;cut();
		pizza-&gt;box();
	};
	virtual Pizza* createPizza(char* type) = 0;
};

class nyPizzaStore : public yh_factoryMethod{
public:
Pizza* createPizza(char* type){
Pizza* pizza;
if (strcmp("cheese", type)){
pizza = new nyCheesePizza();
}
else if (strcmp("papalony", type)){
pizza = new nyPapalonyPizza();
}
}
};

class Pizza{
public:
void prepare();
void bake();
void cut();
void box();

};
class nyCheesePizza : public Pizza{

};
class nyPapalonyPizza : public Pizza{

};
</source>
<br />
4. abstract Factory Pattern이 적용되서 객채의 집합을 생성해주는 방식, 하나의 인터페이스에서 객채군 단위를 생성할때 효율적이다.
- Factory 클래스를 추상으로 제공<br />

- Factory Method 패턴이 공장라인의 부품을 교체할 때 유용한 것이라면 Abstract Factory 패턴은 공장라인 자체를 교체하는 것에 유용하다.<br />

- 다양한 구성 요소 별로 객체의 집합을 생성해야 할 때 유용하다.<br />
<source>
class Pizza{
protected:
	Dough* dough;
	Sauce* sauce;
	Cheese* cheese;
public:
	void prepare();
	void bake();
	void cut();
	void box();

};
class cheesePizza : public Pizza{
yh_abstractFactory* indgredientFactory;
public:
cheesePizza(yh_abstractFactory* indgredientFactory){
cheesePizza::indgredientFactory = indgredientFactory;
};
void prepare(){
dough = indgredientFactory-&gt;createDough();
sauce = indgredientFactory-&gt;createSauce();
cheese = indgredientFactory-&gt;createCheese();
}
};
class yh_abstractFactory{
public:
virtual Dough* createDough() = 0;
virtual Sauce* createSauce() = 0;
virtual Cheese* createCheese() = 0;
};

class NYPizzaIngredientFactory : public yh_abstractFactory{
public:
Dough* createDough(){
return new ThinCrustDough();
};
Sauce* createSauce(){
return new MarinaraSauce();
};
Cheese* createCheese(){
return new ReggianoCheese();
};
};

class Dough{

};
class ThinCrustDough : public Dough{

};
class Sauce{

};
class MarinaraSauce : public Sauce{

};
class Cheese{

};
class ReggianoCheese : public Cheese{

};
</source>
