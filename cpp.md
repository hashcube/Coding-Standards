# C++ conventions

### Compilation

The table below contains the specifics of environment to build the projects. These settings are recommended and please make sure your project and machine matches these specs.

| Topic                    | Config                                              |
|--------------------------|-----------------------------------------------------|
| C++ version              | C++ 14                                              |
| Compiler                 | GCC / CLANG (11.0 +)                                |
| Platforms                | iOS, android, amazon                                |
| Build tools              | CMake (3.6+), gradle for android (5.x), pbx for iOS |
| Compiler flags           | Warnings and Errors                                 |
| Optional libs (external) | Boost                                               |

We are also using CPP check to avoid any false positives in the project. You can easily install it on your system and learn more about it from - http://cppcheck.sourceforge.net/

### Coding Style

**Class name -** use camel case with first upper. eg
``` C++
class Person
{
  // ..
};
```

**local variable name -**  use snake case. eg
``` C++
std::string first_name = “sameer”
```

**member variable name -** use snake case with prefix m_. eg
``` C++
std::string m_first_name;
```

**local class variables -** should be camel case, eg
``` C++
SampleClass sampleObj;
```

**member class variables -** these are member class variables (objects), should be camel case and prefixed with m_.  public class variables should be named as local class variables
``` C++
SampleClass *m_sampleObj;
```

**function names -** use camel case, eg:
``` C++
void doSomethingForMe ()
{
  // ..
}
```

**namespaces -** should be camel case with first letter uppercase:
``` C++
namespace CoreConfig 
{
    // ... 
}
```

**constants -** identifiers should be all caps and words seperated with '_' . eg:
``` C++
const int MIN_AGE = 18;
```

**File Name -** In some places, file can contain multiple class with a main class and small supporting classes, unless these classed are being used by other classes as well, you can keep them in same file to prevent cluttering in file system. The name of the file will be same as the main class in same camel case with first letter uppercase.

**Includes -** CPP includes generally have .hpp extension while C uses .h extension. However, in our case, we will be using .h.
please keep all the includes in .h files only! reason for that is to avoid duplicate include statements, though there will be include guards, that doesn’t look nice, and someone does not have to follow 2 different files to check includes. Also, .h files is where we declare class variables, so having includes there will help you.
ALL .h FILES MUST HAVE INCLUDE GUARDS.

**scope -** start scope {} with new line. eg:
``` C++
namespace SampleNS
{
  class SampleClass : public OtherClass, public AnotherClass
  {
    //..
  };
}
```

for branching and looping, if you have just one statement, and cannot fit in one line, please use scope for it to avoid confusions. eg:
``` C++
for (int i = 0; i < 10; i++)
  if (i % 2 == 0)
    std:;cout << i << std::endl;
```
this will work, however, one must look closely to understand it. Instead this is easy on eyes:
``` C++
for (int i = 0; i < 10; i++)
{
  if (i % 2 == 0)
  {
    std:;cout << i << std::endl;
  }
}
```
however, you can still use inline branching, for eg:
``` C++
if (this->user.getAge() < Globals::MIN_AGE) return false;
```
Max line width is 120 chars. beyond this, you should find a way distribute your code in multiple lines. and indentation = 2 whitespaces.

### Memory Management

C++ allows you to instantiate objects on stack as well as on heap. stack is more controlled memory space which automatically destroys your object out of the scope it is defined in, however heap provides a permanent memory space till the application dies. However, you have to to some manual work to manage this asset.

C++ executes synchronously in a linear fashion. cocos2d-x is on most part executing instructions on a single thread, hence, we can safely presume that initialisation on stack when you require object locally makes more sense. for eg:
``` C++
void SampleClass::sendUserMilestone (User *p_user)
{
  AnalyticsManager am;
  am.sendMessage(“user_ms”, p_user->getCurrentMS());
}
```
After the function ends, the instance of am is automatically destroyed and memory is set free.

This works even when you want to pass the params. for eg:
``` C++
void SomeClass::doSomething ()
{
  OtherClass oc;
  SampleClass sc;
    
  sc.doesSomething(&oc);

  oc.printName();
}
```
Here, you are passing the reference of oc class variable when the function is expecting a reference to the object. remember, as the execution is linear and synchronous, the pointer is valid when the reference is used inside doesSomething var.

However, when you want your instance to be accessed globally, you’ll have to use pointer. for eg.
``` C++
class SampleScene : public cocos2d::Scene
{
private:
  cocos2d::ui::Text* m_currentPage = cocos2d::ui::Text::create();
  
public:
  void setNextPage ()
  {
    std::string page = m_currentPage->getString();
    int nextPage = (static_cast<int>(page) page) + 1;
    m_currentPage->setString(nextPage);
  }
}
```
Now, for us, as we are using cocos, it provides us a safe way to instantiate its classes with create() method, and is when the reference count to that decrements to 0. however, in real world you will have to use new keyword and will require to destroy it with delete keyword. if you don’t, the memory won’t be set free and you will have a memory leak.

### Datatypes and its uses

Make sure whatever data type you use is for a reason. if you use a vector for maintaining an array of fixed length you could as well use an array. if you are using a string, just to store a string of chars locally without performing any operations, you might as well use const char*. std is made for situations where simple datatypes won’t suffice, and using them is expensive.

Sure, you need to use them where they are needed. like rendering a string in button requires you to provide a string and const char*, because pointer evaluation might fail at runtime and string won’t render. hence you will need a more full proof solution.

Please make sure that all member variables are private and not directly available. You will have to write getters and setters for the same.
