# Very, very work in progress.

### This is for adding functions to the source code, not functions for your themes! If you want that, go to the [Theming Help](https://github.com/stepmania/stepmania/wiki#theming-help) section!

### And before you go polluting the source with needless functions, you should check if it can be done in lua first.

On the screen you want to add to, scroll all the way down to where it says "Luna" and then the screen name.

Define your function, such as
```cpp
static int ExampleFunction( T* p, lua_State *L )
{
    COMMON_RETURN_SELF;
}
```

(Lots of information here)

Then in the constructor, add your new function like this
```cpp
ADD_METHOD(ExampleFunction);
```

Finally, add your new function to the StepMania lua documentation. Go to Docs/Luadoc.xml and Docs/LuaDocumentation.xml and add them in the correct places.

In LuaDocumentation.xml
```xml
<Function name='ExampleFunction' return='void' arguments=''>
	A cool example function.
</Function>
```

And LuaDoc.xml
```xml
<Function name='ExampleFunction' />
```