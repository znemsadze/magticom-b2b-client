ჯავა კლინტისთვის საჭიროა keystore. რომლშიც უნდა განთავსდეს, კლიენტის სერთიფიკატი, კლიენტის private key, და სერვერის სერთიფიკატი.
მაგალითად ავიღოთ Let's Encript ის მიერ ხელმოწერილი სერთიფიკატი, 
CSR რექვესტის დადასტურების შემდეგ ვიღებთ ფაილს   fullchain.pem და privkey.pem,

** :~$> openssl pkcs12 -export -out playapp.p12 -inkey privkey.pem -in  fullchain.pem**

მიღებული .p12 შეიძლება დაემატოს ბრაუზერს საკუთარ სერთიფიკატებში, chremes შემთხვევაში 
ვხნით, Settings -> Manage certificates და YOUR CERTIFICATES ჩანართში import ღილაკის მეშვეობით ვტვირთავთ მიღებულ .p12 ფაილს. 
ამის შემდეგ შესაძლებელი იქნება b2b.magticom.ge ზე https არხის გახსნა
და ბრაუზერში swagger ინტერფეისის დათვალიერება,
იმისათვის რომ წვდომადი იყოს მეთოდები საჭიროა თქვენი სერთიფიკატი cert.pem გააგზავნოთ მაგთიკომში რათა მოხდეს მომხმარების რეგისტრაცია.
ჯავა კლიენტისთვის საჭიროა მიღებული *.p12 ფაილი გარდავქმნათ *.jks ფაილად.

** :~$> keytool -importkeystore -srckeystore playapp.p12 -srcstoretype pkcs12  -destkeystore playapp1.jks -deststoretype jks -deststorepass yourPassword**

ამის შემდეგ მიღებულ .jks ფაილში, საჭიროა ჩავამატოთ სერვერის სერთიფიკატი. ამისათვის შეგვიძლია გამოვიყენოთ  კლასი InstallCert,ამ კლასის გაშვებით
ხდება b2b.magticom.ge დან სერთიფიკატის აღება და თქვენს მიერ მითითებულ .jks ფაილში დამატება
ამის შემდეგ SimpleClient   class-ის გაშვებით შეგვიძლია დავრწმუნდეთ რომ ჯავა კლიენტი გაზსნის არხს


for magticom b2b client you need certificate signed by some well known certificate authority,
here is Letsencript Example,

first you need to generate *.p12 file. for that you need fullchain.pem and privkey.pem 

generate *.p12 
** :~$> openssl pkcs12 -export -out playapp.p12 -inkey privkey.pem -in  fullchain.pem**

after you need to generate *.jks

generate *.jks
** :~$> keytool -importkeystore -srckeystore playapp.p12 -srcstoretype pkcs12  -destkeystore playapp.jks -deststoretype jks -deststorepass yourPassword**

then you need to add b2b.magticom.ge server certificate in your *.jks for that purpose you can use InstallCert class
