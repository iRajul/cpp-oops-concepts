# Composite Design Pattern

**Composite** is a structural design pattern that lets you compose objects into tree structures and then work with these structures as if they were individual objects.

![](../../../.gitbook/assets/composite\_diagram.gif)



```cpp
#include <iostream> 
#include <vector>
using namespace std;

class graphics {
    public : 
    virtual void draw () = 0;
    virtual void add(graphics* ref) {};
    virtual ~graphics() {};
};

class line : public graphics {
    int m_num;
    public : 
    line (int num) : m_num(num) {};
    void draw () {
        cout<<"Drawing line : " << m_num <<"\n";
    }
};

class image : public graphics {
    vector<graphics*> childs;
    public :
    void draw() {
        for (auto child : childs) {
            child->draw();
        }
    }
    void add (graphics* child) {
        childs.push_back(child);
    }
};

int main() {
    graphics* img = new image();
    img->add(new line(1));
    img->add(new line(2));
    img->draw();
    return 0;
}
```

* Pros
  * Easier to work with complex composite type. Easier to add new leaf type&#x20;
