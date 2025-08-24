# Multilingual_mobile_app_reviews_2025

Instrukcja dotyczy pgAdmin4

Tworzenie tabeli oraz importowanie pliku do systemu
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

Aby wprowadzić dane należy kliknąć prawym przyciskiem w istniejącą już tabele i wybrać "import/export data"

<img width="1079" height="750" alt="image" src="https://github.com/user-attachments/assets/822ba019-aeb9-4b8d-abc7-b07d25512a19" />
Po wybraniu ścieżki do pliku i wybraniu formatu wybieramy zakładkę option i dostosowujemy ustawienia według zawartości bazy danych. 
Jak widzimy na screenie fragment treści pliku .csv posiada on już headers, więc zaznaczamy je w ustawieniach. Początek i koniec kolumny 
wyznaczają przecinki, dlatego jako delimiter zaznaczamy ten oto znak. Jak możemy też zauważyć w danych występują też cytaty z pełnymi zdaniami i znakami interpunkcyjnymi
dlatego w quote oraz end zaznaczamy cudzysłów aby program wiedział że przecinki w nich powinien zostawić.

<img width="1465" height="121" alt="image" src="https://github.com/user-attachments/assets/8a14fbcd-dd4f-4147-b940-71335a801d1c" />




```sql
select *
from apps_usage
```
<img width="1394" height="583" alt="image" src="https://github.com/user-attachments/assets/4b92a1d0-0922-4e8c-9fa8-7799e73e07f2" />
 tak się prezentuje fragment tabeli po wpisaniu kwerendy.

 Jak widzimy dane udało się wprowadzić i tak prezentuje się fragment tabeli ze wprowadzonymi wszystkich kolumnami

 ```sql
select 
count(distinct app_name) as applications_count
,count(distinct user_country) as countries_count
from apps_usage

```
<img width="425" height="111" alt="image" src="https://github.com/user-attachments/assets/7d473c26-f572-4d7e-937c-591c4f50a33d" />

Aby pokazać zakres danych wpisuje konkretną kwerendę i pokazuje mi, że konkretna baza obejmuje 24 kraje oraz 41 aplikacji. Przechodząc do analizy
moim założeniem jest jakie aplikacje są najpopularniejsze, najwyższej ocenianie ogólnie a później według krajów

na początku można wyświetli top 10 najczęściej ocenianych aplikacji
Wychodzi na to, że najczęściej ocenianią jest Reddit oraz Pinterest. Były ocenianie aż 80 razy.

```sql
select 
app_name
,count(distinct review_id) as number_of_reviews
from apps_usage
group by app_name
order by number_of_reviews desc
limit 10


```
<img width="364" height="367" alt="image" src="https://github.com/user-attachments/assets/818cc9ea-0efe-4a23-a0db-29a67a9cf6f1" />


Jeśli uwzględniemy do tego kraje to największą popularnością cieszy się Microsoft Office w Australii, Pinterest i MX Player w Meksyku oraz eBay w Niemczech.
```sql
select 
user_country as country
,app_name
,count(distinct review_id) as number_of_reviews
from apps_usage
group by app_name, user_country
order by number_of_reviews desc
limit 10
```
<img width="453" height="367" alt="image" src="https://github.com/user-attachments/assets/b8652f69-8f94-4b7c-8531-9c8555233449" />



Aplikacjami z najczęściej występującą najwyższą notą są Lyft oraz Zoom.
```sql
select 
app_name
,rating
,count(rating) number_of_rating
from apps_usage
where rating is not null
group by app_name, rating
order by rating desc, number_of_rating desc
```
<img width="480" height="428" alt="image" src="https://github.com/user-attachments/assets/bfc05ae9-a37b-4e67-b521-886a83a92ea9" />


Można teraz zbadać konkretne trendy m.in. popularność danej aplikacji w konkretnym kraju wyliczając średnią. Uwzględniamy przy tym też recenzje zweryfikowane aby wynik był bardziej wiarygodny.

```sql
select 
app_name
,user_country as country
,round(avg(rating),2) as average_rating
from apps_usage
where rating is not null and verified_purchase ='TRUE' and user_country is not null
group by app_name, user_country
order by average_rating desc
```

<img width="460" height="427" alt="image" src="https://github.com/user-attachments/assets/42a86ee8-4818-459d-a1c8-3b653fc54f83" />






















