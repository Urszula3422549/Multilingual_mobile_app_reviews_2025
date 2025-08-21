# Multilingual_mobile_app_reviews_2025

Instrukcja dotyczy Pgadmin4

<img width="1366" height="706" alt="image" src="https://github.com/user-attachments/assets/76a26452-5840-4113-ad8d-a44919fdff50" />



```sql
create table apps_usage
(
review_id     	integer 
,user_id      	bigint
,app_name     	text
,app_category 	text
,review_text  	text
,review_language 	char(2)
,rating      	numeric(2,1)
,review_date 	timestamp
,verified_purchase 	boolean
,device_type text
,num_helpful_votes integer
,user_age integer
,user_country text
,user_gender text
,app_version text
)
```
<img width="1368" height="532" alt="image" src="https://github.com/user-attachments/assets/e2f8f684-5d47-4a99-a62b-79017890e1cd" />

Klikać prawym przyciskiem myszy w nazwe tabeli i wybrac "import/export data"

<img width="1079" height="750" alt="image" src="https://github.com/user-attachments/assets/822ba019-aeb9-4b8d-abc7-b07d25512a19" />

w zakładce options wybieram jako delimiter przecinek oraz w Quote i escape wybieram cudzysłów, aby program pomijam przecinki pomiędzy nimi.

```sql
select *
from apps_usage
```
<img width="1394" height="583" alt="image" src="https://github.com/user-attachments/assets/4b92a1d0-0922-4e8c-9fa8-7799e73e07f2" />
 tak się prezentuje fragment tabeli po wpisaniu kwerendy.

 ```sql
select 
count(distinct app_name) as applications_count
,count(distinct user_country) as countries_count
from apps_usage

```
<img width="425" height="111" alt="image" src="https://github.com/user-attachments/assets/7d473c26-f572-4d7e-937c-591c4f50a33d" />

Można zobaczyć, że dataset uwzględnia 24 kraje oraz 41 aplikacji.

na początku można zobaczyć w którym kraju dokonano najwięcej recenzji.






