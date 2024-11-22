> **lower_bound, upper_bound 이진탐색으로 원소를 탐색한다.**

### lower_bound

- 찾으려는 key보다 같거나 큰 숫자가 배열의 몇 번째에서 처음 등장하는지 찾기 위함
- 조건 - 오름 차순 정렬
- arr부터 끝까지 탐색하며 6이상의 숫자가 처음 나오는 위치를 반환 없으면 끝 주소값 반환

```C++
int arr[6] = {1,2,3,4,5,6}

cout << "lower_bound(6)" << lower_bound(arr,arr+6, 6) - arr;

int Binary_lower_bound(int s, int e, int number){
    int left=s, right=e;
    int lower_bnd = -1;
    while(left<=right){
        int mid = (left+right)/2;
        if(arr[mid] >= number){
            lower_bnd = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return lower_bnd;
}
```

  

### upper_bound

- 찾으려는 key 값을 초과하는 숫자가 배열 몇 번째에서 처음 등장하는지 찾기 위함
- 조건 - 오름 차순 정렬
- arr부터 끝까지 탐색하며 6을 초과하는 숫자가 처음 나오는 위치를 반환 없으면 끝 주소값 반환

```C++
int arr[6] = {1,2,3,4,5,6}

cout << "upper_bound(6)" << upper_bound(arr,arr+6, 6) - arr;

int Binary_upper_bound(int s, int e, int number)
{
    int left=s,right=e,mid;
    int upper_bnd=-1;
    while (left <= right)
    {
        mid = (left + right) / 2;
        if (arr[mid] <= number)
        {
            upper_bnd = mid;
            left = mid + 1;
        }
        else right = mid - 1;
    }
    return upper_bnd+1 > sizeof(arr) ? -1: upper_bnd+1;
}
```