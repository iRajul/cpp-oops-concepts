# Builder Design Pattern

> To create/instantiate complex & complicated object piecewise & succinctly by providing an API in a separate entity.

* Builder pattern create object in a piece wise manner rather then passing each argument in a constructor.
* Builder Design Pattern also helps in minimizing the number of parameters in constructor & thus there is no need to pass in [null](http://www.vishalchovatiya.com/what-exactly-nullptr-is-in-cpp/?ref=hackernoon.com) for optional parameters to the constructor.
* In below example, we can have a separate class to define steps to create a object as well. So as to create objects with different configurations.

```cpp
#include <iostream> 
#include <vector>
#include <string> 
#include <memory>
using namespace std;

class PersonBuilder;

class Person {
    string m_name; int m_age;
    string m_company_name, m_position;
    Person(const string& name) : m_name (name) {}

    public : 
    friend PersonBuilder;
    static unique_ptr<PersonBuilder> create(const string& name) {
        return  make_unique<PersonBuilder> (name);
    }
};



class PersonBuilder {
    Person m_person;
    public :
    PersonBuilder(const string& name) : m_person (name) {
    }
    operator Person() const {
        return std::move(m_person);
    }

    PersonBuilder* has_age(int age) {
        m_person.m_age = age;
        return this;
    }
    PersonBuilder* works() {
        return this;
    }

    PersonBuilder* with(const string& company) {
        m_person.m_company_name = company;
        return this;
    }

    PersonBuilder* as_a(const string& position) {
        m_person.m_position = position;
        return this;
    }

};

int main() {
    //htmlelement ele =  htmlbuilder("ul");
    //ele.print();
    Person p = Person::create("John")->has_age(41)
        ->works()->with("MG")->as_a("consultant");
    return 0;
}

```
