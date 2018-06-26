# დიზაინ პატერნები და მათი გამოყენება

##### როგორ ვწეროთ უკეთესი კოდი დიზაინ პატერნების დახმარებით

_Bachelors thesis in Computer Sciences. Supervisor: Nino Kiviladze_

## <a name='TOC'>სარჩევი</a>

1.  [რეზიუმე](#abstract)
1.  [შესავალი](#introduction)
1.  [თავი 1: ლიტერატურის მიმოხილვა](#literature_review)
    - [მიმოხილვა](#review_1)
    - [დიზაინ პატერნების სიტორია](#history)
    - [რა არის პატერნი?](#what_is_pattern)
    - [ჩვენ ყოველდღე ვიყენებთ პატერნებს](#everyday_pattern)
    - [Proto-პატერნების ისტორია და "3 წესი"](#proto_patterns)
    - [დიზაინ პატერნების სტრუქტურა](#pattern_structure)
    - [ანტი პატერნები](#anti_patterns)
    - [დიზაინ პატერნების კატეგორიები](#pattern_categories)
      - [Creational კატეგორიის დიზაინ პატერნები](#creational)
      - [Structural კატეგორიის დიზაინ პატერნები](#structural)
      - [Behavioral კატეგორიის დიზაინ პატერნები](#behavioral)
1.  [თავი 2: დიზაინ პატერნები რეალურ პროგრამირებაში](#patterns_in_real)
    - [მიმოხილვა](#review_2)
    - [Round-Trip ინჟინერია VS Single-Page აპლიკაციები](#round_trip_vs_spa)
      - [Round-Trip ინჟინერია](#round_trip_engineering)
      - [Single-Page აპლიკაციები](#spa)
      - [როგორ მუშაობს SPA?](#how_spa_works)
1.  [თავი 3: დიზაინ პატერნები ფრონტ-ენდ ინჟინერიაში](#patterns_in_front_end)
    - [მიმოხილვა](#review_3)
    - [Front-End Framework-ები და დიზაინ პატერნები](#front_end_frameworks)
      - [Angular 2+ დიზაინ პატერნები](#angular_patterns)
    - [Javascript დიზაინ პატერნები](#javascript_patterns)
      - [Constructor პატერნი](#constructor_pattern)
      - [Module პატერნი](#module_pattern)
      - [Singleton პატერნი](#singleton_pattern)
      - [Observer პატერნი](#cobserver_pattern)
      - [Facade პატერნი](#facade_pattern)
      - [Decorator პატერნი](#decorator_pattern)
1.  [შეჯამება](#summarize)

## <a name='abstract'>რეზიუმე</a>

პროგრამირება სულ უფრო და უფრო პოპულარული და მოთხოვნადი ხდება დროთა განმავლობაში. ეს უმეტესწილად განპირობებული არსებული ტექნიკის დამოკიდებულებაზე კომპიუტერულ მეცნიერებასა და პროგრამირებაზე ამან რა თქმა უნდა დახვეწა მიდგომები და სტანდარტები კონკრეტულ პროგრამირების ენებში.

დღესდღეობით პროგრამირება არ მოიცავს ერთი ადამიანის ჩართულობას, პირიქით ერთ პროექტზე შესაძლებელია ათობით და ასობით პროგრამისტი მუშაობდეს. ხოლო პროექტის ჯანსაღი განვითარებისთვის საჭიროა პროგრამისტები მუშაობდნენ ერთად შემუშავებული სტანდარტებით და ნებისმიერი სახის პროგრამულ უზრუნველყოფაზე ჰქონდეთ ისეთი გამოსავალი, რომელიც შემდგომში ხელს არ შეუშლის ახალი ფუნქციონალის დამატებას.

ასევე, ნებისმიერი პროგრამული უზრუნველყოფის შექმნისას, აუცილებელია სწორი და ჩამოყალიბებული არქიტექტურის შემუშავება, რომელიც პროდუქტს გახდის უფრო მოქნილს, გამოყენებადს და გამართულს შემდგომი განვითარებისთვის.

## <a name='introduction'>შესავალი</a>

ამ თეზისში შეფასებული იქნება დიზაინ პატერნები კონკრეტული პროგრამული ენებიდან ასევე ამ პატერნების პრაქტიკული ღირებულება ობიექტზე ორიენტირებულ გარემოში. ასევე განხილული იქნება რა გავლენას ახდენს ე.წ. “Gang of Four(GOF)”-ის სახელით ცნობილი დიზაინ პატერნები ჯავასკრიპტის ერთ-ერთ თანამედროვე ფრეიმვორკზე - Angular-ზე. კვლევა ფოკუსირებული იქნება დიზაინ პატერნების გამოყენების უპირატესობების გამოვლენაზე და ამა თუ იმ პროგრამული ენის მახასიათებლებთან დიზაინ პატერნების შესაძლო კომბინაციების აღმოჩენაზე.

შემდეგი თავი დეტალურად აღწერს პრობლემის არსს და ასევე ნაშრომის მიზანს.

**Problem Statement**

პროგრამირების დროს საკმაოდ რთულია დაიცვა სტანდარტები და წერო ისე, რომ კოდი ყველასათვის გასაგები იყოს. ან თუნდაც შეიმუშავო პრობლემის გადაჭრის ისეთი ხერხი, რომ მან ხელი შეუშალოს და შეაფერხოს ახალი ფუნქციონალის ჩამატება. ამ დროს ხდება ისეთი გამოსავლის მოძებნა, რომელიც არც თუ ისე მართებული და საზოგადოდ მიღებულია.

ნაშრომის მიზანია გამოვიკვლიოთ ზემოთ არსებული პრობლემის მოგვარების ოპტიმალური და საუკეთესო გზა. კერძოდ, განვიხილოთ მიდგომა, რომელსაც Design Patterns ჰქვია. იგი გვთავაზობს საზოგადოდ შექმნილ და არსებულ პრობლემებზე საუკეთესო გამოსავალს და სწორ მიმართულებას. ამასთანავე ნაშრომში განხილულია თანამედროვე და მოწინავე პროგრამული ბიბლიოთეკები და ფრეიმვორკები, რომლებიც მასიურად იყენებენ ამ მიდგომას და ჩაშლილია დეტალურად თითოეული დიზაინ პატერნი, რომელიც გამოყენებულია ამ ბიბლიოთეკებსა თუ პროგრამულ ენებში.

## <a name='literature_review'>თავი 1: ლიტერატურის მიმოხილვა</a>

### <a name='review_1'>მიმოხილვა</a>

ნაშრომის ამ თავში განხილული იქნება “დიზაინ პატერნების” მნიშვნელობა, მისი შემუშავებისა და გამოყენების ისტორია, ასევე უფრო დეტალურად იქნება მოწოდებული თუ რა არის ის უფრო დეტალურად და რას გულისხმობს მისი გამოყენება

### <a name='history'>დიზაინ პატერნების ისტორია</a>

ერთ-ერთი უმნიშვნელოვანესი ასპექტი მართვადი კოდის(maintainable code) წერისა არის ის, რომ შენიშნო განმეორებადი თემები(recurring themes) კოდში და დააოპტიმიზირო ისინი. ეს არის ის სფერო, სადაც დიზაინ პატერნებს შეუძლია დაამტკიცოს მისი ფასდაუდებლობა.

დიზაინ პატერნებს შეგვიძლია მივაკვლიოთ ადრეულ წარსულში მოღვაწე არქიტექტორის - ქრისტოფერ ალექსანდერის(Christopher Alexander) ნამუშევრებში. ის ხშირად წერდა პუბლიკაციებს მისი გამოცდილების შესახებ დიზაინის საკითხების გადაწყვეტაში და როგორ უკავშირდებოდნენ ისინი შენობებსა და ქალაქებს. ერთ დღეს მან აღმოაჩინა, რომ რაც უფრო და უფრო მეტ დროს უთმობდა დიზაინებზე მუშაობას, გარკვეული დიზაინის კონსტრუქციები აშკარა ოპტიმალური ეფექტისკენ მიყავდა.

სარა იშიკასთან(Sara Ishikawa) და მიურეი სილვერსტთან(Murray Silverstein) თანამშრომლობით ალექსანდრემ წარმოადგინა პატერნის(შაბლონის) ენა, რომელიც დაეხმარებოდა ნებისმიერ მსურველს, ვისაც სურდა შეექმნა ნებისმიერი მასშტაბების დიზაინი არქიტექტურაში. იგი წიგნად გამოვიდა 1977 წელს სახელით “A Pattern Language”.

დაახლოებით 30 წლის წინ პროგრამული უზრუნველყოფის ინჟინრებმა(software engineers) დაიწყეს იმ პრინციპების გათვალისწინება და ხმარება, რაც ალექსანდერმა დაწერა თავის პირველ დოკუმენტაციაში დიზაინ პატერნებთან დაკავშირებით,რომელიც უნდა ყოფილიყო სახელმძღვანელო დამწყები დეველოპერებისთვის, რომელთაც სურდათ განევითარებინათ თავიანთი კოდის წერის უნარები.

მნიშვნელოვანია აღინიშნოს, რომ დიზაინის ნიმუშების მიღმა არსებული კონცეფციები პრაქტიკულად შემოფარგლული იყო პროგრამირების ინდუსტრიაში მისივე დასაწყისიდან,თუმცა ნაკლებად ფორმალური ფორმით.

ერთ-ერთი პირველი და ალბათ ყველაზე ღირებული წიგნი, რომელიც დიზაინ პატერნებზე დაიბეჭდა, იყო 1995 წელს დაწერილი წიგნი სახელად “Design Patterns: Elements Of Reusable Object-Oriented Software”. იგი დაწერა 4-მა მეცნიერმა: Erich Gamma, Richard Helm, Ralph Johnson და John Vlissides-მა, რომლებიც ცნობილი გახდნენ როგორც “Gang of Four (GoF)”, რაც ქართულად ითარგმნება როგორც “ოთხთა ბანდა”.

GoF-ის პუბლიკაცია დღემდე ძლიერ ინსტრუმენტად ითვლება დიზაინ პატერნების კონცეფციის ღრმად ჩამოყალიბებასა და დიდი რაოდენობიით დეველოპმენტის ტექნიკისა და პრობლემების აღწერით. ასევე იგი გვთავაზობს საზოგადოდ გავრცელებულ 23 ობიექტზე-ორიენტირებული დიზაინ პატერნის დეტალურ აღწერას. ამ ნაშრომის შემდგომ თავებში უფრო დეტალურად იქნება განხილული ზემოთ ხსენებული დიზაინ პატერნების ძირითადი წარმომადგენლები.

### <a name='what_is_pattern'>რა არის პატერნი?</a>

პატერნი არის მრავალჯერადად გამოყენებადი ამონახსნი, გადაწყვეტა, რომელიც შეიძლება გამოყენებული იქნას ხშირად გამოწვეულ პრობლემებზე პროგრამული უზრუნველყოფის დიზაინში, კერძოდ, ჯავასკრიპტ ვებ აპლიკაციების წერისას. მეორენაირად იგი შეგვიძლია წარმოვიდგინოთ, როგორც პრობლემის გადაწყვეტის (Problem Solve) შაბლონი (Template), რომელიც შეიძლება გამოყენებულ იქნას საკმაოდ განსხვავებულ სიტუაციებშიც კი.

მაშ ასე, რატომ არის მნიშვნელოვანი ჩვენთვის როგორც პროგრამული ინჟინრებისათვის, ვიცოდეთ დიზაინ პატერნები და უფრო ნათელი წარმოდგენა გვქონდეს მათზე?

დიზაინ პატერნებს აქვთ სამი მნიშვნელოვანი სარგებელი:

1.  **პატერნები დადასტურებული გადაწყვეტილებებია** (Patterns are proven solutions): ისინი უზრუნველყოფენ პროგრამული უზრუნველყოფის განვითარებაში აპრობირებული მეთოდების გამოყენებით მყარი პრობლემის გადაწყვეტის მიდგომებს.

1.  **პატერნები შესაძლებელია მარტივად იქნას განმეორებით გამოყენებული** (patterns can be easily reused): პატერნი, როგორც წესი, ასახავს “out of the box” გამოსავალს, რომელიც შეიძლება ადაპტირებული იყოს ჩვენი მოთხოვნილებების დასაკმაყოფილებლად. ეს ფუნქცია ხდის მათ საკმაოდ მოქნილს და ძლიერს.

1.  **პატერნები შეიძლება იყოს გამომხატველი** (Patterns can be expressive): როდესაც პატერნს შევხედავთ დავინახავთ,რომ წარმოდგენილია გადაწყვეტა სტრუქტურითა და შესაბამისი ლექსიკით (Vocabulary), რომელსაც შეუძლია გამოხატოს ბევრად მეტი გადაწყვეტები საკმაოდ ელეგანტურად.

უნდა გავითვალისწინოთ, რომ პატერნები **არ არის ზუსტი** ამონახსნი კონკრეტულ პრობლემაზე. მნიშვნელოვანია გვახსოვდეს, რომ პატერნების როლი არის ის რომ უბრალოდ წარმოგვიდგინოს გადაწყვეტის სქემა (Solution Scheme). პატერნები არ წყვეტენ ყველა დიზაინთან არსებულ პრობლემას, არც კარგ პროგრამულ ინჟინრებს ანაცვლებენ, თუმცა საკმაოდ “ეხმარებიან” მათ.

- **განმეორებით პატერნების გამოყენება ხელს უწყობს უმნიშვნელო საკითხების თავიდან აცილებას, რამაც შეიძლება მნიშვნელოვანი პრობლემები გამოიწვიოს აპლიკაციის განვითარების პროცესში.**
  ეს იმას ნიშნავს, რომ როცა პროგრამული კოდი აგებულია აპრობირებულ პატერნებზე, შეგვიძლია ნაკლები დრო დავუთმოთ კოდის სტრუქტურაზე წუხილს და ფიქრს, პირიქით უფრო მეტი დრო დავუთმოთ და მეტი აქცენტი გავაკეთოთ საერთო გადაწყვეტის (Overall Solution) ხარისხზე. ეს იმიტომაა, რომ დიზაინის წინასწარ განსაზღვრული შაბლონები საშუალებას გვაძლევს კოდი ვწეროთ უფრო სტრუქტურირებული და ორგანიზებული სახით, რაც შესაბამისად იძლევა საშუალებას მომავლისთვის თავიდან აცილებული იქნას კოდის რეფაქტორირება სისუფთავის მიზნით.

- **პატერნებს შეუძლია უზრუნველყონ განზოგადებული გადაწყვეტები, რომლებიც ისეთი სახითაა დოკუმენტირებული, რომ სრულიად არ საჭიროებენ რომელიმე კონკრეტულ პრობლემასთან კავშირს.** ეს განზოგადებული მიდგომა ნიშნავს იმას, რომ მიუხედავად პროგრამისა (და ხშირ შემთხვევაში პროგრამირების ენა) რომელზეც ვმუშაობთ, დიზაინის ნიმუშები შეიძლება გამოყენებულ იქნას ჩვენი კოდის სტრუქტურის გასაუმჯობესებლად.

- **ზოგიერთ პატერნს რეალურად შეუძლია შეამციროს საერთო კოდის მოცულობა, კოდის გამეორების (Code Repetition) თავიდან აცილების გზით.**
  თუ დეველოპერები გულდასმით დაუფიქრდებიან მათ გადაწყვეტილებებს კონკრეტულ პრობლემებზე, შეეძლებათ საგრძნობლად შეამცირონ კოდის მოცულობა. მაგალითად: შეამცირონ ბევრი ფუნქცია-მეთოდების რაოდენობა, ერთი, განზოგადებული ფუნქციის ხარჯზე, რომელიც იდეურად და ფუნქციონალურად იმავეს ემსახურება რასაც ბევრი მეთოდი ცალ-ცალკე. ასევე ცნობილია, როგორც გახადო კოდი რაც შეიძლება [“DRY(Don’t Repeat Yourself)”](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

- **პატერნები, რომლებიც ხშირად გამოიყენება, დროთა განმავლობაში შეიძლება გაუმჯობესდეს კოლექტიური გამოცდილების გამოყენებით რომელსაც სხვა დეველოპერები იყენებენ, და გაუმჯობესებული სახით დაუბრუნდეს დიზაინ პატერნების საზოგადოებას.**
  ზოგიერთ შემთხვევებში ეს იწვევს სრულიად ახალი პატერნის ჩამოყალიბებას, ხოლო სხვა შემთხვევებში კი იწვევს გაუმჯობესებულ მითითებებს, თუ როგორ შეიძლება კონკრეტული პატერნები საუკეთესოდ იქნას გამოყენებული. ეს ყველაფერი კი ჯამში ამყარებს იმ აზრს, რომ პატერნებზე დაფუძნებული გადაწყვეტილებები აგრძელებენ გახდნენ უფრო მტკიცე და სტრუქტურირებული, ვიდრე კონკრეტულ პრობლემაზე მორგებული გადაწყვეტები.

### <a name='everyday_pattern'>ჩვენ ყოველდღე ვიყენებთ პატერნებს</a>

უკეთ რომ გავიაზროთ რამდენად საჭირო და სასარგებლოა დიზაინ პატერნები, განვიხილოთ მარტივი ელემენტის ამოღების(select) პრობლება რომელსაც jQuery ბიბლიოთეკა ჩვენთვის წყვეტს.

წარმოვიდგინოთ გვაქვს სკრიპტი, სადაც თითოეულ DOM-ში ნაპოვნი ელემენტისთვის, რომელსაც class ექნება “foo” ჩვენ ქაუნთერს(counter) ვზრდით ერთით. რა იქნება ყველაზე მოსახერხებელი და ეფექტური გზა იმისთვის რომ შესაბამისი ბრძანება(query) დავწეროთ? ამ პრობლემის გადასაჭრელად არსებობს რამდენიმე გზა.

1.  ამოვიღოთყველაელემენტივებ-გვერდიდანდაშევინახოთმათზე მიმთითებლები (References). შემდეგ, გავფილტროთ ეს კოლექცია და გამოვიყენოთ regular expressions იმისთვის, რომ მხოლოდ დაგვიტოვოს ის ელემენტები, რომლებსაც კლასად აქვთ “foo”.

1.  გამოვიყენოთთანამედროვებრაუზერებისერთ-ერთიშესაძლებლობა, როგორიცაა **`querySelectorAll()`** ამოვირჩიოთ ყველა ის ელემენტი რომელსაც ექნება კლასი “foo”.

1.  ანგამოვიყენოთმშობლიურიშესაძლებლობა,როგორიცაა **`getElementsByClassName()`** რომ მივიღოთ იგივე შედეგი რაც ზემოთ მოყვანილ მაგალითებში.

მაშ ასე, რომელია ამ სამი შემოთავაზებიდან ყველაზე სწრაფი? ეს არის მე-3, მაგრამ რეალურ აპლიკაციაში შეაძლოა მე-3 ვარიანტმა არ იმუშაოს Internet Explorer-ის ძველ ვერსიებში, ამრიგად საჭიროა ხანდახან გამოვიყენოთ 1, მაშინ როცა არც მე-2 და არც მე-3 არ არის მოწყობილობის მიერ მხარდაჭერილი.

დეველოპერებს, რომლებიც jQuery-ს იყენებენ, ისინი ამ გამოწვევის წინაშე არ დგანან, რადგანაც საბედნიეროდ ეს პრობლემა გადაწყვეტილია `Facade Pattern`-ის საშუალებით. ამ პატერნს მომავალში უფრო დაწვრილებით განვიხილავთ, მაგრამ მანამდე: ეს პატერნი გვთავაზობს მარტივი აბსტრაქტირებული ინტერფეისების ერთობლიობას (მაგ. <span style="color:#e6005c
">$el.css()</span> , <span style="color:#e6005c
">$el.animate()</span> ) შედარებით რთული და კომპლექსური კოდისათვის. ეს კი ჩვენ საშუალებას გვაძლევს ნაკლებად ვიფიქროთ შიდა შრეების იმპლემენტაციის დეტალებზე.
ამ ყველაფრის უკან, ბიბლიოთეკა უბრალოდ ეძებს ყველაზე ეფექტურ გამოსავალს კლიენტის ბრაუზერისა და პროგრამული მხარდაჭერის გათვალისწინებით.
ალბათ ყველასათვის ცნობილია jQuery-ის <span style="color:#e6005c
">$(“selector”)</span> სინტაქსი. იგი არის ყველაზე მარტივი და მოსახერხებელი გზა HTML ელემენტების ასარჩევად, განსხვავებით ზემოთ ჩამოთვლილი ალტერნატივებისგან : <span style="color:#e6005c
">getElementById()</span> , <span style="color:#e6005c
">getElementsByClassName()</span> , <span style="color:#e6005c
">getElementsByTagName()</span> და ასე შემდეგ.

### <a name='proto_patterns'>Proto-პატერნების ისტორია და "3 წესი"</a>

უნდა გვახსოვდეს რომ ყველა ალგორითმი ან საუკეთესო პრაქტიკა ან პრობლემის გადაწყვეტის გზა არ შეიძლება ჩაითვალოს დიზაინ პატერნად. შეიძლება არსებობდეს ისეთი პატარა ინგრედიენტები რომლებიც ზემოთ ჩამოთვლილთ აკლდეს, რის გამოც იგი სრულყოფილ პატერნად არ ჩაითვალოს.

Alexander-ის სიტყვები რომ გავიხსენოთ, იგი ამბობდა რომ პატერნი უნდა იყოს ორივე: პროცესიც და “რაღაცაც” (thing), და იგი ამ გამოთქმაში მართალი იყო, რადგან პატერნი არის სწორედ ის პროცესი რაც ქმნის “რაღაცას”. ამიტომაც არის ხოლმე, უმეტესწლიად პატერნი წარმოდგენილია როგორც ვიზუალურად შედგენილი სტრუქტურა.

როდესაც დიზაინ პატერნებს ვსწავლობთ არ უნდა გაგვიკვირდეს, როცა შეგვხვდება ტერმინი “proto-pattern”. რა არის იგი? პატერნი რომელიც ჯერ არ არის მზად რომ “pattern”-ity ტესტი ჩააბაროს, იგულისხმება რომ იგი არის proto-pattern. პროტო- პატერნები შეიძლება მივიღოთ ერთი ჩვეულებრივი ადამიანის მუშაობისგან, რომელმაც მოიფიქრა და შეიმუშავა კონკრეტული გადაწყვეტა პრობლემის , რაც ძალზედ ღირებული იქნება საზოგადოებისთვის გასაზიარებლად.

სრულყოფილი პატერნის შესამუშავებლად და დოკუმენტირებისთვის აუცილებელი რამდენიმე რამ გავითვალისწინოთ. მაგალითად: პატერნი შეიძლება ჩაითვალოს “კარგად” მაშინ როცა იგი აკმაყოფილებს შემდეგს:

- **ჭრის კონკრეტულ პრობლემას** : პატერნები არ არის იმისთვის, რომ ჩამოაყალიბონ მშრალი პრინციპები და სტრატეგიები. ისინი კონკრეტულ გადაჭრის გზას ეხმიანებიან. ეს არის ერთ-ერთი მთავარი ინგრედიენტი კარგი პატერნისთვის.

- **გადაჭრის გზა კონკრეტული პრობლემისთვის არ უნდა იყოს ცხადი**

- **აღწერილი კონცეპტი აუცილებლად უნდა იყოს დამტკიცებული:** დიზაინ პატერნები საჭიროებენ იმის მტკიცებულებას, რომ ისინი ზუსტად ისე ფუნქციონირებენ როგორც აღწერილია, წინააღმდეგ შემთხვევაში ეს პატერნები სერიოზულად აღქმული ვერ იქნება.

- **იგი უნდა აღწერდეს კავშირს, ურთიერთობას:** პატერნის ოფიციალურმა აღწერამ დეტალურად და ღრმად უნდა აღწეროს სისტემის სტრუქტურა და მექანიზმები, რომლებიც ხსნიან მათ კავშირს კოდთან.

ასევე, დამატებითი მოთხოვნილება რომ პატერნი იყოს ვალიდური, არის ის, რომ ისინი აჩვენებენ განმეორებად ფენომენს. ეს ხშირად არის ის, რაც შეგიძლია სამ პუნქტად ჩამოაყალიბო, ანუ “The Rule Of Three” . ესენია:

1.  **Fitness of purpose** - რამდენად წარმატებულად ითვლება პატერნი?

1.  **Usefulness** -რატომ ითვლება წარმატებულად პატერნი?

1.  **Applicability**- იმსახურებს დიზაინი რომ იყოს პატერნი იმიტომ რომ ფართო გამოყენება აქვს? თუ კი, მაშინ ეს უნდა იქნას დასაბუთებული.

### <a name='pattern_structure'>დიზაინ პატერნების სტრუქტურა</a>

დიზაინ პატერნების სტრუქტურაში უკეთ გასარკვევად, თვალი გადავავლოთ იმ ელემენტებს რომლებიც პატერნისთვის აუცილებელი და დამახასიათებელია. დიზაინ პატერნს უნდა ჰქონდეს:

- **Pattern name** - პატერნის სახელი და აღწერა.
- **Context Outline** - კონტექსტი, რომელშიც ნიმუში ეფექტურია მომხმარებლების მოთხოვნებზე რეაგირებაში.
- **Problem Statement** - პრობლემის აღწერიდან უნდა გამომდინარეობდეს რა არის პატერნის განზრახვა.
- **Solution** - აღწერა, თუ როგორ ხდება მომხმარებლის პრობლემის გადაჭრა გასაგებად აღწერილი ნაბიჯებით.
- **Design** - ნიმუშის დიზაინის აღწერა და კერძოდ, მომხმარებლის ქცევა მასთან ურთიერთქმედებაში.
- **Implementation** - გზამკვლევი თუ როგორ უნდა განვახორციელოთ პატერნი კონკრეტულ პროექტში.
- **Illustrations** - პატერნში შემავალი კლასების ვიზუალური წარმოდგენა (მაგ. დიაგრამა).
- **Examples** - მინიმალისტურ ვარიანტში პატერნის იმპლემენტაციის მაგალითი.
- **Relations** - რომელი პატერნები წააგავს ამ პატერნს? მსგავსია იგი სხვის?
- **Known usage** - გამოიყენება თუ არა პატერნი სხვაგანაც? თუ კი, სად და როგორ?
- **Discussions** -გუნდის ან ავტორის მოსაზრებები პატერნის საინტერესო სარგებელზე.

დიზაინ პატერნები არის საკმაოდ მძლავრი მიდგომა ორგანიზაციაში მყოფი ყველა
დეველოპერის გასაერთიანებლად მაშინ, როცა ისინი მუშაობენ საერთო ამოცანაზე.

იმ შემთხვევაში თუ თქვენ მუშაობთ საკუთარი პატერნის შექმნაზე , გახსოვდეთ, რომ მიუხედავად იმისა, რომ დაგეგმვისა და ჩაწერის პროცესის თავდაპირველი დროითი დანახარჯი შესაძლოა გაიზარდოს, ამ ინვესტიციიდან დაბრუნებული შედეგი საკმაოდ ფასეულია და ამართლებს წინასწარი სამუშაოების გახანგრძლივებას.

სანამ მუშაობას დავიწყებთ პატერნებზე, უმჯობესია ჯერ კვლევა ჩავატაროთ, რადგან შეიძლება აღმოვაჩინოთ უფრო სასრგებლო პატერნი, რომელზეც შეგვეძლება ახალი შესაძლებლობების დამატება, ვიდრე ყველაფრის ნულიდან დაწყება.

### <a name='anti_patterns'>ანტი პატერნები</a>

თუ ჩავთვლით,რომ პატერნი წარმოადგენს საუკეთესო პრაქტიკას, ანტი-პატერნი წარმოადგენს გაკვეთილს, რომელიც ვისწავლეთ. ტერმინი ანტი-პატერნები პირველად გამოყენებულ იქნა 1995 წელს Andrew Koenig-ის მიერ.
მის ნაშრომში წარმოდგენილია ანტი-პატერნის ორი ცნება, ესენია:

- ანტი-პატერნები აღწერენ ცუდ გადაწყვეტას (Bad Solution) კონკრეტულ პრობლემაზე, რის შედეგადაც მოხდა ცუდი სიტუაცია
- ანტი-პატერნები აღწერენ როგორ დავაღწიოთ თავი აღნიშნული სიტუაციიდან და ცუდი გადაწყვეტიდან კარგ გადაწყვეტილებამდე მივიდეთ.

მაშინ, როცა ძალიან მნიშვნელოვანია პატერნების ცოდნა, თანაბრად მნიშვნელოვანია ასევე ანტი-პატერნების ცოდნაც. ამის მიზეზი კი შემდეგში მდგომარეობს: როდესაც აპლიკაციას ვქმნით, პროექტის სასიცოცხლო ციკლი იწყება კონსტრუქციით (Construction), მაგრამ მაშინ როცა მზად იქნება პროექტის პირველადი release ვერსია, საჭიროა, რომ იგი შენარჩუნებული (Maintained) იყოს. საბოლოო გადაწყვეტილების ხარისხი: კარგი იქნება თუ ცუდი, დამოკიდებულია შესაძლებლობების დონესა და დროზე რაც ჩადო გუნდმა მასში. აქ ცუდი და კარგი პატერნი განიხილება კონტექსტში (Context). “საუკეთესო” დიზაინიც კი შეიძლება კვალიფიცირდეს, როგორც ანტი-პატერნი, თუ იგი გამოყენებული იქნება არასწორ კონტექსტში.

დიდი გამოწვევები იწყება მაშინ,როცა აპლიკაცია აღწევს წარმოებამდე, ანუ გადის production-ში.დეველოპერი, რომელიც მუშაობ ამ პროექტზე, რომელსაც აქამდე არ უმუშავია მსგავს სისტემებზე, შესაძლოა რომ შემთხვევით პროექტში “ცუდი” დიზაინი შეიმუშავოს. თუ ვამბობთ, რომ ცუდი პრაქტიკები იქმნებიან როგორც ანტი-პატერნები, მაშინ შეგვიძლია ვთქვათ, რომ ისინი დეველოპერებს აძლევენ საშუალებას რომ ისინი წინასწარ გაეცნონ მად და თავიდან აიცილონ საერთო შეცდომები, რომლების შესაძლოა გამოჩნდეს- ეს პარარელურია იმ მიდგომისა, სადაც დიზაინ პატერნები გვაწვდიან გზას რომ წინასწარ გავეცნოთ საერთო ტექნიკებს, რომლების სასარგებლოა პროდუქტის განვითარებისთვის.

რომ შევაჯამოთ, ანტი-პატერნი არის ცუდი დიზაინი, რომელიც საჭიროებს რომ დოკუმენტირებული იყოს, რათა დეველოპერმა წინასწარ იცოდეს ის და მუშაობის პროცესში იგივე შეცდომა არ დაუშვას.

ქვემოთ წარმოგიდგენთ ანტი-პატერნების რამდენიმე მაგალითს ჯავასკრიპტში(Javascript)

- გლობალურ კონტექსტში დიდი რაოდენობით ცვლადების განსაზღვრით გლობალური namespace-ის დაბინძურება.
- ფუნქციის ნაცვლად სტრინგის გადაწოდება setTimeout და setInterval მეთოდებზე, რადგან იგი იწვევს eval() ფუნქციის გამოძახებას იძულებით
- Object class prototype-ის შეცვლა
- Document.write- ის გამოყენება მიუხედავად native DOM-ის სხვა ალტერნატივებისა. მაგ. Document.createElement.

ანტი-პატერნების ცოდნა სასიცოცხლოდ მნიშვნელოვანია წარმატებისთვის. მას შემდეგ, რაც გვეცოდინება ეს ანტი-პატერნები,ჩვენ შეგვეძლება რომ კოდს ჩავუტაროთ რეფაქტორირება იმისთვის რომ თავიდან ავიცილოთ და უარვყოთ ისინი, რაც შესაბამისად გააუმჯობესებს ჩვენი გადაწყვეტილებების ხარისხს მყისიერად.

### <a name='pattern_categories'>დიზაინ პატერნების კატეგორიები</a>

დიზაინ პატერნები შეიძლება ჩაშლილი იყოს სხვადასხვა კატეგორიებად. ამ თავში განვიხილავთ 3 ძირითად კატეგორიას და მოკლედ მიმოვიხილავთ იმ პატერნებს, რომლებიც ერთიანდებიან ამ კატეგორიებში.

##### <a name='creational'>Creational კატეგორიის დიზაინ პატერნები</a>

creational დიზაინ პატერნები ფოკუსირდებიან ობიექტის შექმნის(object creation) მექანიზმის მართვაზე, სადაც ობიექტები იქმნებიან ისე, როგორც ეს მუშაობის დროს არსებული სიტუაციისთვის არის შესაფერისი. ობიექტის შექმნის ძირითადმა მიდგომამ შეიძლება გამოიწვიოს დამატებითი სირთულეები პროექტში, ხოლო ამ პატერნების მიზანია გადაჭრან ეს პრობლემა შექმნის პროცესის გაკონტროლებით.

პატერნები, რომლებიც ამ კატეგორიაში გადიან არის: **Constructor**, **Factory**, **Abstract**, **Prototype**, **Singleton** და **Builder**.

##### <a name='structural'>Structural კატეგორიის დიზაინ პატერნები</a>

Structural პატერნები დაინტერესებული არიან ობიექტის შემადგენლობით და როგორც წესი, გამოკვეთენ მარტივ გზებს იმის გასაანალიზებლად, თუ როგორ არიან დაკავშირებული ერთმანეთთან სხვადასხვა ობიექტები. ისინი გვეხმარებიან იმის უზრუნველყოფაში, რომ სისტემის ერთ ნაწილში ცვლილებების შემთხვევაში, არ უნდა იყოს საჭიროება იმის რომ მთელი სისტემის სტქრუქტურა შეიცვალოს.

პატერნები, რომლებიც ამ კატეგორიაში გადიან, არის: **Decorator**, **Facade**, **Adapter** და **Proxy**.

##### <a name='behavioral'>Behavioral კატეგორიის დიზაინ პატერნები</a>

behavioral დიზაინ პატერნები ფოკუსირებული არიან სისტემის განსხვავებულ
ობიექტებს შორის კომუნიკაციის გაუმჯობესებაზე ან გამარტივებაში.

Behavioral პატერნები მოიცავს: **Iterator**, **Mediator**, **Observer** და **Visitor**.

იმისათვის, რომ უფრო ნათელი გახდეს დიზაინ პატერნების კატეგორიებად კლასიფიკაცია, ქვემოთ მოყვანილია შესანიშნავი ცხრილი ამასთან დაკავშირებით:

|                         |                                                                                                                                               |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Creational**          | Based on the concept of creating an object.                                                                                                   |
| _**Class**_             |
| Factory Method          | This makes an instance of several derived classes based on interfaced data or events.                                                         |
| _**Object**_            |
| Abstract Factory        | Creates an instance of several families of classes without detailing concrete classes.                                                        |
| Builder                 | Separates object construction from its representation, always creates the same type of object.                                                |
| Prototype               | A fully initialized instance used for copying or cloning.                                                                                     |
| Singleton               | A class with only a single instance with global access points.                                                                                |
| **Structural**          | Based on the idea of building blocks of objects.                                                                                              |
| _**Class**_             |
| Factory Method          | Match interfaces of different classes therefore classes can work together despite incompatible interfaces.                                    |
| _**Object**_            |
| Adapter                 | Match interfaces of different classes therefore classes can work together despite incompatible interfaces.                                    |
| Bridge                  | Separates an object's interface from its implementation so the two can vary independently.                                                    |
| Composite               | A structure of simple and composite objects which makes the total object more than just the sum of its parts.                                 |
| Decorator               | Dynamically add alternate processing to objects.                                                                                              |
| Facade                  | A single class that hides the complexity of an entire subsystem.                                                                              |
| Flyweight               | A fine-grained instance used for efficient sharing of information that is contained elsewhere.                                                |
| Proxy                   | A place holder object representing the true object.                                                                                           |
| **Behavioral**          | Based on the way objects play and work together.                                                                                              |
| _**Class**_             |
| Interpreter             | A way to include language elements in an application to match the grammar of the intended language.                                           |
| Template Method         | Creates the shell of an algorithm in a method, then defer the exact steps to a subclass.                                                      |
| _**Object**_            |
| Chain of Responsibility | A way of passing a request between a chain of objects to find the object that can handle the request.                                         |
| Command                 | Encapsulate a command request as an object to enable, logging and/or queuing of requests, and provides error-handling for unhandled requests. |
| Iterator                | Sequentially access the elements of a collection without knowing the inner workings of the collection.                                        |
| Mediator                | Defines simplified communication between classes to prevent a group of classes from referring explicitly to each other.                       |
| Observer                | A way of notifying change to a number of classes to ensure consistency between the classes.                                                   |
| State                   | Alter an object's behavior when its state changes.                                                                                            |
| Strategy                | Encapsulates an algorithm inside a class separating the selection from the implementation.                                                    |
| Visitor                 | Adds a new operation to a class without changing the class.                                                                                   |
