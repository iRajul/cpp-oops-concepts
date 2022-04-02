# 😀 Dependency Inversion Principle

> * _High-level modules should not depend on low-level modules. Both should depend on abstractions._
> * _Abstractions should not depend on details. Details should depend on abstractions._



Lets take a scenario where a User want to reset password. So we design password reset which is dependent upon interface to database rather then concrete `MysqlDB` .&#x20;

It helps to change database to other in future. This way High level module `PasswordReset` is dependent on low level module `DBInterface`

```cpp
#include <iostream>
#include <memory>
using namespace std;

class DBInterface {
	public: 
	virtual bool connect ()  = 0 ;
};
class MysqlDB : public DBInterface  {
	public:
	virtual bool connect() {
		cout<<"connected"<<endl;
		return true;
	}
};

class PasswordReset {
	shared_ptr<DBInterface> m_db;
	public:
	PasswordReset(shared_ptr<DBInterface>& database) : m_db(database) {
		m_db->connect();
	}
};
int main() {
	shared_ptr<DBInterface> db(new MysqlDB());
	PasswordReset pr(db);
	return 0;
}
```
