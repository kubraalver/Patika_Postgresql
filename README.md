[Sample Database](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/)
# ÖDEV 1
**1. film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.**

        SELECT title, description FROM film;

**2. film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.**

        SELECT * FROM film 
        WHERE length > 60 and length < 75;

**3. film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.**

        SELECT * FROM film 
        WHERE rental_rate = 0.99 AND (replacement_cost = 12.99 OR replacement_cost = 28.99);

**4. customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?**
   
        Smith

**5. film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.**

        SELECT * FROM film 
        WHERE length <= 50 AND rental_rate NOT IN (2.99, 4.99);


# ÖDEV 2
**1. film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)**

        SELECT * FROM film 
        WHERE replacement_cost BETWEEN 12.99 AND 16.99 AND replacement_cost NOT IN (16.99);
   
**2. actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)**
  
        SELECT first_name, last_name FROM actor
        WHERE first_name IN ('Penelope', 'Nick', 'Ed');

**3. film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)**
  
        SELECT * FROM film
        WHERE rental_rate IN (0.99, 2.99, 4.99) AND replacement_cost IN (12.99, 15.99, 28.99);

# ÖDEV 3
**1. country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.**

        SELECT * FROM country
        WHERE country LIKE 'A%a';

**2. country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.**

        SELECT * FROM country
        WHERE country LIKE '_____%n';

**3. film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.**

        SELECT * FROM film
        WHERE title ILIKE '%t%t%t%t%';

**4. film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.**

        SELECT * FROM film
        WHERE title LIKE 'C%' AND length > 90 AND rental_rate = 2.99;

# ÖDEV 4

**1. film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.**

        SELECT DISTINCT replacement_cost FROM film;

**2. film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?**

        SELECT COUNT (DISTINCT replacement_cost) FROM film;

**3. film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?**

        SELECT COUNT(*) FROM film
        WHERE title LIKE 'T%' AND rating = 'G';

**4. country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?**

        SELECT COUNT (*) FROM country
        WHERE country LIKE '_____';

**5. city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?**

        SELECT COUNT (*) FROM city
        WHERE city ILIKE '%r';

# ÖDEV 5

**1. film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.**

        SELECT * FROM film
        WHERE title LIKE '%n'
        ORDER BY length DESC
        LIMIT 5;

**2. film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.**

        SELECT * FROM film
        WHERE title LIKE '%n'
        ORDER BY length ASC
        OFFSET 5
        LIMIT 5;

**3. customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.**

        SELECT * FROM customer
        WHERE store_id = 1
        ORDER BY last_name DESC
        LIMIT 4;

# ÖDEV 6

**1. film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?**

        SELECT AVG(rental_rate) FROM film;

**2. film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?**

        SELECT COUNT(*) FROM film
        WHERE title LIKE 'C%';

**3. film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?**

        SELECT MAX(length) FROM film
        WHERE rental_rate = 0.99;
        
**4. film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?**

        SELECT COUNT(DISTINCT replacement_cost) FROM film
        WHERE length > 150;
        
# ÖDEV 7

**1. film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.**

        SELECT rating FROM film
        GROUP BY rating;

**2. film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.**

        SELECT replacement_cost, COUNT(replacement_cost) FROM film
        GROUP BY replacement_cost
        HAVING COUNT(*) > 50;

**3. customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir?**

        SELECT store_id,COUNT(*) FROM customer
        GROUP BY store_id;

**4. city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.**

        SELECT country_id, COUNT(*) FROM city
        GROUP BY country_id
        ORDER BY COUNT(*) DESC
        LIMIT 1;
# ÖDEV 8
**1. test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.**

        CREATE TABLE employee (
        	id INTEGER,
        	first_name VARCHAR(50) NOT NULL,
        	last_name VARCHAR(50) NOT NULL,
        	birthday DATE,
        	email VARCHAR(100)
        );

**2. Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.**

        insert into employee (id, first_name, last_name, birthday, email) values (1, 'Mateo', 'McAlister', '1979-10-15', 'mmcalister0@google.de');
        insert into employee (id, first_name, last_name, birthday, email) values (2, 'Douglass', 'Degenhardt', '2008-06-26', 'ddegenhardt1@kickstarter.com');
        insert into employee (id, first_name, last_name, birthday, email) values (3, 'Willem', 'Jurkowski', '2015-04-06', 'wjurkowski2@patch.com');
        insert into employee (id, first_name, last_name, birthday, email) values (4, 'Mack', 'De Ferrari', '2020-06-20', 'mdeferrari3@hubpages.com');
        insert into employee (id, first_name, last_name, birthday, email) values (5, 'Margo', 'Maffioni', '1996-06-11', 'mmaffioni4@cbc.ca');
        insert into employee (id, first_name, last_name, birthday, email) values (6, 'Petronella', 'Tandy', '1983-11-17', 'ptandy5@illinois.edu');
        insert into employee (id, first_name, last_name, birthday, email) values (7, 'Wilburt', 'MacKibbon', '1974-12-21', 'wmackibbon6@surveymonkey.com');
        insert into employee (id, first_name, last_name, birthday, email) values (8, 'Wilma', 'Robertsson', '1993-10-11', 'wrobertsson7@goo.ne.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (9, 'Arabele', 'Formilli', '2001-02-22', null);
        insert into employee (id, first_name, last_name, birthday, email) values (10, 'Nicolette', 'Arnaudi', '1981-07-22', 'narnaudi9@prweb.com');
        insert into employee (id, first_name, last_name, birthday, email) values (11, 'Haslett', 'Fergie', '2004-03-11', 'hfergiea@businessinsider.com');
        insert into employee (id, first_name, last_name, birthday, email) values (12, 'Roman', 'Crosher', '2001-05-22', 'rcrosherb@nih.gov');
        insert into employee (id, first_name, last_name, birthday, email) values (13, 'Averil', 'Dossett', '2007-06-16', 'adossettc@cisco.com');
        insert into employee (id, first_name, last_name, birthday, email) values (14, 'Rey', 'Nutley', '1971-01-09', 'rnutleyd@techcrunch.com');
        insert into employee (id, first_name, last_name, birthday, email) values (15, 'Victoria', 'Kneller', '2008-08-28', 'vknellere@yahoo.co.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (16, 'Camey', 'Smale', '2001-08-11', 'csmalef@princeton.edu');
        insert into employee (id, first_name, last_name, birthday, email) values (17, 'Chadd', 'Baumadier', '1995-02-04', 'cbaumadierg@cbslocal.com');
        insert into employee (id, first_name, last_name, birthday, email) values (18, 'Nicholas', 'Lergan', '2017-08-25', 'nlerganh@multiply.com');
        insert into employee (id, first_name, last_name, birthday, email) values (19, 'Alejandra', 'Jeayes', '2012-10-03', 'ajeayesi@printfriendly.com');
        insert into employee (id, first_name, last_name, birthday, email) values (20, 'Orlando', 'Niaves', '1974-06-14', 'oniavesj@rediff.com');
        insert into employee (id, first_name, last_name, birthday, email) values (21, 'Crosby', 'Cullingford', '2005-12-20', 'ccullingfordk@dion.ne.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (22, 'Di', 'Antonignetti', '2017-11-05', 'dantonignettil@rambler.ru');
        insert into employee (id, first_name, last_name, birthday, email) values (23, 'Georas', 'Pegden', '1981-07-18', 'gpegdenm@howstuffworks.com');
        insert into employee (id, first_name, last_name, birthday, email) values (24, 'Sandra', 'Fitt', '2022-03-09', null);
        insert into employee (id, first_name, last_name, birthday, email) values (25, 'Nikolaos', 'Lintill', '1995-06-13', 'nlintillo@linkedin.com');
        insert into employee (id, first_name, last_name, birthday, email) values (26, 'Ashien', 'Heminsley', '1971-12-30', 'aheminsleyp@purevolume.com');
        insert into employee (id, first_name, last_name, birthday, email) values (27, 'Kai', 'Beacom', '1975-09-26', 'kbeacomq@goo.ne.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (28, 'Rafa', 'Larver', '2020-05-14', 'rlarverr@skype.com');
        insert into employee (id, first_name, last_name, birthday, email) values (29, 'Tawnya', 'Caret', '1980-04-18', null);
        insert into employee (id, first_name, last_name, birthday, email) values (30, 'Tymon', 'Growcock', '2019-09-10', 'tgrowcockt@mysql.com');
        insert into employee (id, first_name, last_name, birthday, email) values (31, 'Arlina', 'Muckersie', '2000-02-25', 'amuckersieu@twitter.com');
        insert into employee (id, first_name, last_name, birthday, email) values (32, 'Letty', 'Vernalls', '1999-09-06', 'lvernallsv@msn.com');
        insert into employee (id, first_name, last_name, birthday, email) values (33, 'Patience', 'Woolaghan', '2012-01-29', 'pwoolaghanw@vkontakte.ru');
        insert into employee (id, first_name, last_name, birthday, email) values (34, 'Gretta', 'Tatershall', '1984-04-25', 'gtatershallx@amazon.co.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (35, 'Vinson', 'Sheryn', '1987-10-25', 'vsheryny@netscape.com');
        insert into employee (id, first_name, last_name, birthday, email) values (36, 'Alfi', 'Agron', '2001-05-10', 'aagronz@cdbaby.com');
        insert into employee (id, first_name, last_name, birthday, email) values (37, 'Darrelle', 'Grigoletti', '1987-08-10', 'dgrigoletti10@sina.com.cn');
        insert into employee (id, first_name, last_name, birthday, email) values (38, 'Annalee', 'Prine', '1991-08-18', 'aprine11@topsy.com');
        insert into employee (id, first_name, last_name, birthday, email) values (39, 'Lynn', 'Dog', '1995-01-12', 'ldog12@examiner.com');
        insert into employee (id, first_name, last_name, birthday, email) values (40, 'Ripley', 'Harbison', '1984-05-11', 'rharbison13@exblog.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (41, 'Brita', 'Barneville', '2006-07-13', 'bbarneville14@multiply.com');
        insert into employee (id, first_name, last_name, birthday, email) values (42, 'Juliet', 'Beynon', '2014-06-25', 'jbeynon15@ox.ac.uk');
        insert into employee (id, first_name, last_name, birthday, email) values (43, 'Luz', 'Stammer', '2005-02-11', 'lstammer16@amazonaws.com');
        insert into employee (id, first_name, last_name, birthday, email) values (44, 'Conrad', 'Linacre', '1979-01-18', 'clinacre17@salon.com');
        insert into employee (id, first_name, last_name, birthday, email) values (45, 'Lucretia', 'Chazerand', '2015-11-18', 'lchazerand18@ovh.net');
        insert into employee (id, first_name, last_name, birthday, email) values (46, 'Daniel', 'Wordesworth', '2006-01-11', 'dwordesworth19@eepurl.com');
        insert into employee (id, first_name, last_name, birthday, email) values (47, 'Ray', 'Haugeh', '1983-06-23', 'rhaugeh1a@japanpost.jp');
        insert into employee (id, first_name, last_name, birthday, email) values (48, 'Ki', 'Siggens', '2004-09-14', 'ksiggens1b@timesonline.co.uk');
        insert into employee (id, first_name, last_name, birthday, email) values (49, 'Randell', 'Elen', '2008-06-30', 'relen1c@cbc.ca');
        insert into employee (id, first_name, last_name, birthday, email) values (50, 'Nicolai', 'Fer', '1996-07-14', 'nfer1d@istockphoto.com');

**3. Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.**

        UPDATE employee
        SET first_name = 'Matt'
        WHERE first_name = 'Mateo'
        RETURNING *;
        
        UPDATE employee
        SET last_name = 'Crosh'
        WHERE id = 12
        RETURNING *;
        
        UPDATE employee
        SET birthday = '2000-08-25'
        WHERE last_name = 'Lergan'
        RETURNING *;
        
        UPDATE employee
        SET first_name = 'xxxx'
        WHERE birthday = '2020-06-20'
        RETURNING *;
        
        UPDATE employee
        SET email = 'xxx@yyy.com'
        WHERE last_name = 'Tandy'
        RETURNING *;

**4. Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.**

        DELETE FROM employee
        WHERE id = 3;
        
        DELETE FROM employee
        WHERE first_name = 'Petronella';
        
        DELETE FROM employee
        WHERE last_name = 'Fergie';
        
        DELETE FROM employee
        WHERE birthday = '2020-06-20';
        
        DELETE FROM employee
        WHERE email = 'ddegenhardt1@kickstarter.com';
