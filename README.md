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
