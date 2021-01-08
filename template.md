## print vector

```C++
template<class T>
    void printvector(vector<T> const vec){
        for(int i: vec) std::cout << i << " ";
        std::cout << std::endl;
    }

```

## print matrix

```C++
    template<class T>
    void printMatrix(std::vector<std::vector<T>> const vec){
        for(std::vector<T> v: vec){
            for(int i: v){
                std::cout << i<<" ";
            }
            std::cout << std::endl;
        }
    }
```

## max

```C++
    int max(int a, int b){
        return (a>b)?a:b;
    }
```

## 初始化一个m*n的0矩阵

```C++

    std::vector<std::vector<int>> res (m, std::vector<int>(n,0));



```