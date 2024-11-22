- [**Compare vs ==**](https://choryeonworkshop.tistory.com/119)
    
    ```C++
    //string
    int compare (const string& str) const noexcept;
    
    //substrings
    int compare(size_t pos, size_t len, const string& str) const;
    int compare (size_t pos, size_t len, const string& str,
                 size_t subpos, size_t sublen = npos) const;
                 
    // c-string
    int compare (const char* s) const;
    int compare (size_t pos, size_t len, const char* s) const;
    
    // buffer
    int compare (size_t pos, size_t len, const char* s, size_t n) const;
    ```
    
    **return vlaue → compare : 이게 바로 차이점**
    
    - 0 : 두 문자열이 같다
    - < 0 : 일치하지 않는 첫 번째 문자의 값이 비교할 문자열의 값보다 더 낮다.  
        or 모든 문자가 일치하지만 비교할 문자열이 더 짧다.  
        
    - > 0 : 일치하지 않는 첫 번째 문자의 값이 비교할 문자열의 값보다 더 크다  
        or 모든 문자가 일치하지만 비교할 문자열이 더 길다.  
        
    
    ## 결론 : == , compare은 같다? ==같다!==
    
    ```C++
    string s = "hello";
    string s3 = "hello";
    
    char c[6] = "hello";
    
    string *s1 = new string;
    s1->append("hello");
    
    string &s2 = s;
    
    cout << (s == *s1) << endl;
    cout << (s == c) << endl;  
    cout << (s == s2) << endl;
    cout << (s == s3) << endl;
    
    cout << endl;
    
    cout << (s.compare(*s1) == 0) << endl;
    cout << (s.compare(c) == 0) << endl;  
    cout << (s.compare(s2) == 0) << endl;
    cout << (s.compare(s3) == 0) << endl;
    
    
    // 결과
    1
    1
    1
    1
    
    1
    1
    1
    1
    ```
    
    > **그럼 왜??**
    
- [**형변환**](https://blockdmask.tistory.com/334)
    
    **string → int : stoi**
    
    **char* → int : atoi**