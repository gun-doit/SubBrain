# 사용한 색 조합
  
![[Pasted image 20241227170949.png]]
#F8FAFC

#D9EAFD

#BCCCDC

#9AA6B2
[flex 공식 블로그](https://flex.team/blog/category/article/)
# TODO
- [ ] 다크모드 구현
- [ ] About페이지 구현
- [x] 사이트 조회수
- [x] 게시글 조회수
- [ ] SEO 최적화
- [ ] 무한스크롤 구현
![[Pasted image 20250108095804.png]]
#### /blog
: 블로그 메인페이지
- [ ] github 잔디 연동
- [ ] 조회수 그래프
- [ ] 블로그 게시물 확인
- [ ] 카테고리

#### /post/[category]/[id]
: 블로그 게시물 페이지
- [x] 게시물 뷰

## BackEnd API
#### 블로그
- [ ] 전체 카테고리 불러오기
- [ ] 특정 게시물 불러오기
- [ ] 게시물 검색
- [x] 카카오 로그인 구현


## DB
: 몽고DB, postgrl db
스키마
```
const HealthSchema = new mongoose.Schema({
    userId: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User',
        required: true
    },
    pushup_total: {
        type: Number,
        default: 0
    },
    pullup_total: {
        type: Number,
        default: 0
    },
    pushup_data: [{
        date: {
            type: Date || Date.now,
        },
        sets: [{
            setNumber: Number,
            count: Number
        }],
        totalCount: Number
    }],
    pullup_data: [{
        date: {
            type: Date || Date.now,
        },
        sets: [{
            setNumber: Number,
            count: Number
        }],
        totalCount: Number
    }]
}, {
    timestamps: true
});
```

[{
userId;
pushup_total: number
pullup_total : number
pushup_data:
	{
	data:
	sets: []
	totalCount	
	}
pullup_data:
	{
	data:
	sets: []
	totalCount	
	}
}]