# design
模式
//单例模式
class singleton
{
public:
	static singleton instance()
	{
		if (mpsingleton == NULL)
		{
			mpsingleton = new singleton();
		}
		return mpsingleton;
	}
private:
	singleton(){}
	static singleton *mpsingleton;
};
singleton::mpsingleton = NULL;


//观察者监听者模式
class listener
{
public:
	listener(string name):_name(name){}
	virtual void handlmessage(int message) = 0;
	//纯虚函数 拥有纯虚函数的类成为抽象类

protected:
	string _name;
};

class listener1 : public listener
{
	listener1(string name):listener(name){}
	//从基类继承成员变量 调用基类构造方法初始化该变量
	void handlmessage(int msgid)
	{
		switch(msgid)
		{
		case 0:cout<<"0 interested!"<<endl;
		case 1:cout<<"1 interested!"<<endl;
		case 2:cout<<"2 interested!"<<endl;
		}
	}
}

class listener2 : public listener
{
	listener2(string name):listener(name){}
	//从基类继承成员变量 调用基类构造方法初始化该变量
	void handlmessage(int msgid)
	{
		switch(msgid)
		{
		case 0:cout<<"0 interested!"<<endl;
		case 2:cout<<"2 interested!"<<endl;
		}
	}
}

class listener2 : public listener
{
	listener2(string name):listener(name){}
	//从基类继承成员变量 调用基类构造方法初始化该变量
	void handlmessage(int msgid)
	{
		switch(msgid)
		{
		case 1:cout<<"1 interested!"<<endl;
		case 2:cout<<"2 interested!"<<endl;
		}
	}
}

class observe
{
public:
	void registerlistener(listener *p,int msgid)
	//基类指针指向派生类成员 正确
	{
		_obmap[msgid]->push_back(p);
	}
	void displaymessage(int msgid)
	{
		map<int,list<listener*>>::iterator it =
			_obmap.find(msgid);
		if (it != _obmap.end())
		{
			list<listener *>::iterator it1 = it->second->begin();
			for (;it1 != it->second->end();it1++)
			{
				(*it1).handlmessage(msgid);
			}
		}
	}
private:
	map<int,list<listener*>> _obmap;
	int msgid;
};
