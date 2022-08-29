---
layout: default
title: oop design pattern builder
parent: oop
nav_order: 406108
---

- 객체 생성 작업을 대신해줄 클래스를 추가하는 패턴

- 복합 객체의 생성 과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴

- 객체 생성이 복잡하거나 여러 개의 추가 작업이 필요한 경우 유용함
<source>
#include <stdio.h>
class Item
{
private:
	char* sword;
	char* armor;
public:
	void setSword(char* swordType)
	{
		sword = swordType;
	}
	void setArmor(char* armorType){
		armor = armorType;
	}
	void printItem(){
		printf("%s\n",sword);
		printf("%s\n", armor);
	}
};

class yh_builder
{
protected:
Item* item;
public:
Item getItem(){
return *item;
}
void createItem(){
item = new Item();
}
virtual void buildSword() = 0;
virtual void buildarmor() = 0;
};

class metalItemBuilder : public yh_builder
{
public:
void buildSword(){
item-&gt;setSword("metalSword");
}
void buildarmor(){
item-&gt;setArmor("metalArmor");
}
};

class blackSmith
{
private:
yh_builder *builder;
public:
void setItem(yh_builder* itemBuilder){
builder = itemBuilder;
}
Item getItem(){
return builder-&gt;getItem();
}
void constructure(){
builder-&gt;createItem();
builder-&gt;buildarmor();
builder-&gt;buildSword();
}
};
</source>
<source>
int main()
{
	blackSmith *smith = new blackSmith();
	metalItemBuilder *metal = new metalItemBuilder();
	smith->setItem(metal);
	smith->constructure();

	Item i = smith-&gt;getItem();
	i.printItem();

	return 0;
}
</source>

----
