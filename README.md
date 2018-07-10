Sebastian Cojocariu 321CB UPB ACS					
  
			                         Real-Time-Filter-Content

Idee (schita):
-vom folosi Visitor Design Pattern pentru a interpreta o expresie booleana data in prefix(ca in tema,insa algoritmul prezentat merge si
pentru infix).
-vom folosi Observer Design Pattern pentru a trimite feed-uri/a inregistra/a sterge/... observeri.
-vom folosi Factory Design Pattern atat pentru a genera Noduri in mod Dinamic,cat si pentru a creea Observeri(aceasta fabrica va fi si Singleton).
-vom folosi Singleton Design Pattern cand cream clasa CalculatorVisitor ce implementeaza Visitor.

Package NodeType: 
	-Clasa Data contine un String si un double reprezentand name-ul,respectiv value-ul care se vor actualiza la fiecare feed.
	-Clasa Node contine referinte catre Node left,respectiv Node right,cat si un camp Data ce va fi folosit in cadrul Operand-ului.
	-Avem aici toate cele 9 tipuri de noduri : AndNode,OrNode,Operand,EqNode,NeNode,LtNode,LeNode,GtNode,GeNode.Fiecare dintre aceste clase 
mosteneste clasa Node si implementeaza interfata Visitable(adica implementeaza metoda accept din Visitable).Clasa Operand are diversi constructori pentru
a actualiza campul data din Node(celelalte tipuri de noduri nu vor folosi acest camp).
	-CalculatorVisitor este un Singleton care implementeaza interfata Visitor(deci implementeaza fiecare metoda visit cu cele 9 tipuri de Noduri 
primite ca parametru).
	-NodeFactory respecta conditiile din Factory Design Pattern si contine metoda getNode(String s) care returneaza un anumit tip de node(in functie de
stringul s primit ca parametru).

Package Observer:
	-clasa PrefixToPostfix contine metoda getPostfix(String s) ce converteste expresia booleana s din infix sau prefix in postfix.
(A se vedea algoritmul din cod)
	-clasa CreateArbore contine campul Data data si Node start.Totodata,mai are metoda getArbore(String s) care primeste un string s reprezentand
o expresie booleana in format postfix si creeaza arborele binar aferent expresiei,actualizand start cu "inceputul" arborelui.Ideea centrala pentru
a optimiza verificarea a fost sa introducem campul Data care,la fiecare actualizare,va modifica parametri din arbore ce tin de ea(name si value)
,fara a mai fi nevoie sa refacem la fiecare pas arborele(practic arborele se va creea o singura data,iar prin modificarea parametrilor din campul data
modificam efectiv in arbore value/name).Metoda check returneaza valoarea expresiei din arborele tinut in start avand drept date(value si name) campul data. 
	-clasa ObserverFactory este un Singleton si respecta Factory Design Pattern.Contine metoda getObserver(Subject stockGrabber,String filter,
int observerID) ce genereaza un observer pentru Subjectul stockGrabber,cu filtrul filter(String) si cu id-ul observerID,facand legaturile corespunzatoare
(inregistreaza acest observer la subjectul respectiv,ii da id-ul corespunzator,creeaza arborele aferent filtrului,etc)
	-clasa Info contine informatiile pentru un stoc anume(va fi folosit in fiecare treemap al fiecarui observer):valoarea curenta a stocului,
valoarea stocului la ultimul print dat,numarul de fluctuatii de la ultimul print dat si procentul fluctuatiei dintre cele 2 valori de la cele 2 printuri. 
	-interfetele Subject,respectiv Observer
	-clasa StockGrabber implementeaza Subject
	-clasa ConcreteObserver implementeaza Observer

	
