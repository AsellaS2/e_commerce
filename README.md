# e_commerce
![](https://github.com/AsellaS2/e_commerce/assets/69001369/2b32ef3a-af32-4c9c-beb5-9a7682574bf7)

---

사용데이터
-   [Amazon Canada Products](https://www.kaggle.com/datasets/asaniczka/amazon-canada-products-2023-2-1m-products/data) 및 [Amazon India Products](https://www.kaggle.com/datasets/asaniczka/amazon-india-products-2023-1-5m-products)
-   [MUSINSA 뷰티/ 신발 data](https://www.musinsa.com/categories/item/005)

---

###Q1.list price 가격과 판매가 차이 [26.8%](https://www.busan.com/view/busan/view.php?code=20000511000159) 나는 제품은 얼마나 있는가?

```
listPrice = in_data['listPrice']
price = in_data['price']

reas_price_df = in_data[in_data['price']<=in_data['listPrice']*0.732]


reas_price_category = reas_price_df.groupby('categoryName')['categoryName'].count()
reas_price_category=reas_price_category.sort_values(ascending=False)
reas_price_category.head(10)
```

|categoryName|---|
|---|---|
पुरुषों के हैट्स और कैप्स |12306
मेकअप|10754|
खेल, फिटनेस और आउटडोर|9400
MP3 प्‍लेयर आर्मबैंड|9344
होम और किचन|8920
महिलाओं की लॉन्जरी और नाइटवियर|8328
रकसैक और ट्रेकिंग बैकपैक|7919
ट्रैवल एक्सेसरीज़|7803
बालों की देखभाल|7771
सूटकेस, चेक इन और स्ट्रॉली|7519
Name: categoryName, dtype: int64

---
힌디어를 번역해보자
```
from googletrans import Translator


translator = Translator()

Top_10_categoryName = reas_price_category[0:10].index
# src는 입력언어,  dest는 원하는 출력언어 

for i in Top_10_categoryName:
    print(i)
    a = translator.translate(i, src='hi', dest='ko')
    print(a.text)
```

나온 결과
### A:
할인을 하는 가격으로 판매되는 품목 카테고리 top10 아래와

|순위|categoryName|
|---|---|
1순위|पुरुषों के हैट्स और कैप्स
1순위|남자 모자와 모자
2순위|मेकअप
2순위|조립
3순위|खेल, फिटनेस और आउटडोर
3순위|스포츠, 피트니스 및 야외
4순위|MP3 प्‍लेयर आर्मबैंड
4순위|MP3 플레이어 완장
5순위|होम और किचन
5순위|가정과 주방
6순위|महिलाओं की लॉन्जरी और नाइटवियर
6순위|여성은 더 길고 나이트웨어입니다
7순위|रकसैक और ट्रेकिंग बैकपैक
7순위|Raksack과 트레킹 배낭
8순위|ट्रैवल एक्सेसरीज़
8순위|여행 액세서리
9순위|बालों की देखभाल
9순위|헤어 케어
10순위|सूटकेस, चेक इन और स्ट्रॉली
10순위|여행 가방, 체크인 및 빨대

---
반대로 할인하지 않지만 많이 파는 품목은 무엇일까?

```
review_stars_df

reas_price_df = review_stars_df[review_stars_df['price']<=review_stars_df['listPrice']]

###
reas_not_price_category = reas_price_df.groupby('categoryName')['categoryName'].count()
reas_not_price_category=reas_not_price_category.sort_values()
reas_not_price_category.head(10)
```

나온 결과 :

### A: 정찰제와 비슷한 가격으로 판매될 가능성이 많은 품목 카테고리 top10 위와 같다

|순위|categoryName|
|---|---|
|1순위|रनिंग GPS यूनिट
|1순위|실행 GPS 장치
|2순위|पुरुषों के स्पोर्ट्स कोट और ब्लेज़र्स
|2순위|남성 스포츠 코트와 블레이저
|3순위|Gamezone
|3순위|Gamzon
|4순위|Skin care
|4순위|피부 관리
|5순위|Pain relief
|5순위|통증 완화
|6순위|फ़ाइन आर्ट
|6순위|미술
|7순위|महिलाओं के ड्रेसेस और जंपसूट्स
|7순위|여자 드레스와 점프 수트
|8순위|डिजिटल SLR कैमरे
|8순위|디지털 SLR 카메라
|9순위|Vitamins & Supplements - Pharmacy
|9순위|비타민 및 보충제 - 약국
|10순위|स्पोर्ट्स कलेक्‍टिबल
|10순위|스포츠 수집가

---
할인을 많이 하는 품목 중 하나인 헤어 케어 항목을 무신사 데이터에서도 수집해 보았다.

그렇게 아마존 인도와 무신사의 헤어케어 항목에 대한 상관계수는 아래와 같다.


#### indea hair care corr

|()| price |in_stars |review|
|---|---|---|---|          
price | 1.00 | 0.01 | 0.09
in_stars|0.01| 1.00|0.08
review|0.09|0.08|1.00


#### musinsa hair care corr

|()| price |in_stars |review|
|---|---|---|---|  
price | 1.000000| -0.070175|-0.059726
stars | -0.070175 | 1.000000 | 0.897146
review | -0.059726| 0.897146|1.000000
