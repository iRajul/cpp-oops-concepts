# Bridge Pattern

#### Intent

`Decouple an abstraction from its implementation so that the two can vary independently.`

![\[1\]](../../../.gitbook/assets/bridgediagram.png)

* Pimple Idiom is example of Bridge pattern where implementation is hide from client using implementation class.&#x20;
* Another example is given below :&#x20;

```
#include <iostream> 
using namespace std;
class shape;
class renderer {
    public :
    virtual void render_square(const shape& ref) const = 0;
};

class rasterRenderer : public renderer{
    public :
    virtual void render_square(const shape& ref) const {
        cout<<"Raster renderer\n";
    }
};

class shape {
    public :
    virtual void draw() const = 0;
};

class square : public shape {
    private :
        const renderer& m_renderer;
    public :
    square(const renderer &renderObj) : m_renderer (renderObj) {}
    virtual void draw () const {
        m_renderer.render_square(*this);
    }
};

int main() {
    rasterRenderer raster;
    square squareObj(raster);
    squareObj.draw();
    return 0;
}
```

&#x20;&#x20;

When to use?&#x20;

* Use the Bridge pattern when you want to divide and organize a monolithic class that has several variants of some functionality (for example, if the class can work with various database servers).
* Use the Bridge if you need to be able to switch implementations at runtime. It makes it similar to Strategy pattern.

High level abstraction and low level implementation can be separated using this pattern.&#x20;

* Pros&#x20;
  * [x] SRP
  * [x] OCP

\[1] Image reference : [bogotobogo](https://www.bogotobogo.com/DesignPatterns/bridge.php)

