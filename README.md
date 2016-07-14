# GetClassInnerType
```java


    private static Type getSuperGenericClass(Class<?> klass) {
        return klass.getGenericSuperclass();
    }

    private static <T> Class<T> getType(Class<?> clz) {
        Type type = getSuperGenericClass(clz);
        return getRealType(type);
    }

    private static <T> Class<T> getRealType(Type type) {
        Class<T> c = null;
        if (type instanceof ParameterizedType) {
            Type[] types = ((ParameterizedType) type).getActualTypeArguments();
            if (types != null && types.length > 0) {
                Type t = types[0];
                if (t != null && t instanceof ParameterizedType) {
                    c = getRealType(t);
                } else {
                    c = ((Class<T>) t);
                }
            }
        }
        return c;
    }
    public static void main(String[] args) {
        ArrayList<ArrayList<String>> str=new ArrayList<ArrayList<String>>(){};
        str.add(new ArrayList<>());

        Class c=getType(str.getClass());

        System.out.println(c.getName());
        System.out.println(c.getSimpleName());
    }
    
    
    Result:
    java.lang.String
    String
    
```
