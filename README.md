Δήμα Μαρία

ΑΜ Π2013029

Μάθημα: HCI

Εργασία: Data Visualization (# D3js-uk-political-donations)


Παραδοτέο1:

λινκ στο αποθετήριο του κώδικα: https://github.com/p13dima/D3js-uk-political-donations

λινκ στο κλαδί του κώδικα που αντιστοιχεί στο παραδοτέο: https://github.com/p13dima/D3js-uk-political-donations/tree/2013029-Paradoteo1

λινκ στο εκτελέσιμο: https://p13dima.github.io/D3js-uk-political-donations/full-viz


- [X]  Ο σύνδεσμος της σελίδας σας με την εφαρμογή.

- [ ]	 Εφαρμόστε τις κατάλληλες αλλαγές έτσι ώστε το url της εφαρμογής σας να μην χρειάζεται να καταλήγει σε "full-viz.html" (π.χ. από Mitsos.github.io/D3js-uk-political-donations/full-viz.html σε Mitsos.github.io/D3js-uk-political-donations/).

Δεν λειτουργεί παρότι χρησιμοποιώ το gh-pages branch και το έχω ορίσει ως πηγή στο GitHub Pages στα Settings του αποθετηρίου.


- [X]  Αλλαγή χρωμάτων στις μπάλες με τα δεδομένα, καθώς και στα αντίστοιχα 3 πεδία της ομαδοποίησης Split by party.

Στο αρχείο chart.js, Γραμμή 24 , αλλαγή από:

var fill = d3.scale.ordinal().range(["#F02233", "#087FBD", "#FDBB30"]);

σε:

var fill = d3.scale.ordinal().range(["#002233", "#F87FBD", "#0DBB30"]);

Κόκκινο--> Μαύρο
Μπλέ--> Ροζ
Κίτρινο--> Πράσινο

Οι γραμμές 154-164 του αρχείου style.css δεν παίζουν ρόλο.

Στο αρχείο style.css, Γραμμές 63-76:

/*  Party view */
#conservative, #labour, #libdem { padding: 10px; }
#conservative {
    background: rgba(8, 127, 189, 0.2);
    top: 110px;
}
#labour {
    background: rgba(240, 34, 51, 0.2);
    top: 330px;
}
#libdem {
    background: rgba(253, 187, 48, 0.2);
    top: 550px;

αλλαγή των χρωμάτων σε:

    background: rgba(255, 190, 189, 0.2);

    background: rgba(0, 0, 0, 0.2);
    
    background: rgba(50, 187, 48, 0.2);
    
    
- [X]	 Να ακούγεται ήχος κάθε φορά που ο χρήστης της εφαρμογής κάνει κλικ σε μία από τις επιλογές/κουμπιά ομαδοποίησης των δεδομένων.

o	Προσθήκη αρχείο click.wav

o	Στο αρχείο full-viz.html προσθέτω στη γραμμή 37:
	 <audio id="audioElement" src="click.wav"></audio>
και στα a tags των li των γραμμών 43, 45, 47, 49 προσθέτω το:
onclick="document.getElementById('audioElement').play()"

- [X]	 Τροποποιήστε τον κώδικα έτσι ώστε όταν κάνετε κλικ σε κάθε μπάλα να ανοίγει ένα νέο παράθυρο με τα αποτελέσματα της αναζήτησης στο google για τον αντίστοιχο δωρητή.

•	Στο αρχείο chart.js, Γραμμή 95 , προσθήκη:

```.on("click", mouseclick)```

•	Και στη Γραμμή 351, προσθήκη:

```function mouseclick(d, i) {```
	```// tooltip new_tab```
	```var mosie = d3.select(this);```
	```var donor = d.donor;```
```	window.open('https://www.google.gr/search?safe=active&q='+ donor, '_blank');```
```}```

- [X]	 Ορισμένοι από τους αναγνώστες της εφαρμογής ενδεχομένως να είναι άτομα με περιορισμένη όραση. Τροποποιήστε τον κώδικα της εφαρμογής έτσι ώστε το ποντίκι να λειτουργεί και ως μεγεθυντικός φακός όταν μεταφέρεται επάνω από τις λέξεις του κειμένου.

Προσθήκη 2 μορφοποιήσεων (κλάσεων) στο CSS:
```div.magnifiable:hover { font-size: 150%; }```
```div.magnifiable_width:hover { font-size: 150%; width: 170%}```

Και στον html κώδικα προσδιορισμός της επιθυμητής κλάσης σε κάθε div. Π.χ.
```<div id="f" class="magnifiable">```
Αν κάποιο στοιχείο κειμένου δεν βρίσκεται μέσα σε div το συμπεριλαμβάνουμε σε ένα. Π.χ.
```<div class="magnifiable">```
        ```<h1>Who's funding the big three?</h1> </div>```

Η δεύτερη κλάση (magnifiable_width) είναι μια εναλλακτική της πρώτης όπου αυξάνει (κατά 170%) και το πλάτος της οντότητας. Χρησιμοποιήθηκε σε περιπτώσεις μεγάλου κειμένου όπου η μεγέθυνση αύξανε κατά πολύ τις γραμμές του κειμένου και επικάλυπτε οντότητες που βρίσκονται πιο κάτω στην σελίδα


ΕΝΑΛΛΑΚΤΙΚΑ, ΜΕ ΧΡΗΣΗ της D3:
Προσθήκη των παρακάτω συναρτήσεων στο ```<head>``` <script> του full-viz.html:
	
```function magnify(t,s) {
	d3.selectAll(t).style('text-anchor', 'middle')
		.on('mouseover', function(d,i) {
			d3.select(this).style('font-size', (s+10)+'px')	})
		.on('mouseout', function(d,i) {
			d3.select(this).style('font-size', s+'px') });	
}
```
	
```function magnify_Width(t,s) {
	d3.selectAll(t).style('text-anchor', 'middle')
		.on('mouseover', function(d,i) {
			d3.select(this).style('font-size', (s+10)+'px')
			d3.select(this).style('width', '170%')	})
		.on('mouseout', function(d,i) {
			d3.select(this).style('font-size', s+'px')
			d3.select(this).style('width', '100%')	});
}
```

Το πρώτο όρισμα δηλώνει σε ποια οντότητα της html θέλουμε να γίνει η μεγέθυνση και το 2ο σε ποιο μέγεθος κειμένου θέλουμε να επανέλθει (άρα το αρχικό μέγεθος του στοιχείου που μεγεθύνουμε). Η μεγέθυνση γίνεται κατά 10px μεγαλύτερη γραμματοσειρά.
Η δεύτερη συνάρτηση είναι μια εναλλακτική της πρώτης όπου αυξάνει (κατά 170%) και το πλάτος της οντότητας. Χρησιμοποιήθηκε σε περιπτώσεις όπου η μεγέθυνση αύξανε κατά πολύ τις γραμμές του κειμένου και επικάλυπτε οντότητες που βρίσκονται πιο κάτω στην σελίδα.

Ενώ και η παρακάτω γραμμή κώδικα ΠΡΕΠΕΙ να μεταφερθεί από το τέλος του αρχείου (γραμμή 209) στην κορυφή (μέσα στο <head>):

```<script src="//cdnjs.cloudflare.com/ajax/libs/d3/3.2.2/d3.v3.min.js" charset="utf-8"></script>```

Κλήση των συναρτήσεων που δημιουργήσαμε σε όλα τα κείμενα της html. Π.χ.:

```<script>
			magnify_Width('h2', 24);	
			magnify_Width('p', 16);	
		</script>
```
ή
```	<script>magnify_Width('#conservative', 16);</script>```
ή
```	<script>magnify('#company', 16);</script>```
κλπ.



- [X] Για τον ίδιο λόγο, τροποποιήστε τον κώδικα της εφαρμογής έτσι ώστε όταν το ποντίκι βρίσκεται μέσα στον κύκλο κάποιου δωρητή, να ακούγεται η ονομασία του δωρητή και το ποσό της δωρεάς.
Προσθήκη του παρακάτω κώδικα στο αρχείο chart.js στο τέλος της συνάρτησης mouseover() (Γραμμή 348):
```	var msg = new SpeechSynthesisUtterance(donor);
	window.speechSynthesis.speak(msg);
	var msg = new SpeechSynthesisUtterance(comma(amount)+"pounds");
	window.speechSynthesis.speak(msg);
```
Χρήση του Speech Synthesis Web API 


- [X] Δημιουργήστε τουλάχιστον μία ακόμα επιλογή ομαδοποίησης των δεδομένων (π.χ. Split by the amount of the donatio).

Παρόμοια με το group by source type.
Στο αρχείο chart.js προστέθηκαν:
Νέες θέσεις στο entityCentres
Νέα περίπτωση για το div "group-by-amount" στην transition function
Και οι συναρτήσεις amountType, amounts και moveToAmounts για τη δημιουργία του νέου γραφήματος.
