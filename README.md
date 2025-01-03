# ΑΣΚΗΣΗ 1 (1η Εργαστηριακή Άσκηση 2024-25.pdf)
Πανεπιστήμιο Πατρών  
Τμήμα Μηχ. Η/Υ & Πληροφορικής  

Στατιστική Επεξεργασία Σήματος και Μάθηση  

Πρώτη Εργαστηριακή Άσκηση  
Ακαδημαϊκό Έτος 2024/25  

**Ταυτοποίηση άγνωστου συστήματος (System Identification)**

Στην παρούσα εργασία θα ασχοληθούμε με ένα από τα βασικότερα προβλήματα της στατιστικής επεξεργασίας σημάτων και μάθησης (με πληθώρα εφαρμογών), που είναι η ταυτοποίηση ενός αγνώστου συστήματος (system identification), το οποίο μπορεί, γενικώς, να είναι και χρονικά μεταβαλλόμενο. Η διαδικασία της ταυτοποίησης πραγματοποιείται με την εκτίμηση των συντελεστών του αγνώστου συστήματος.

## 1. Γραμμικό Χρονικά Αμετάβλητο Σύστημα

![Εικόνα 1](https://github.com/nickpotamianos/STATISTIKI_EPEKSERGASIA_SIMATWN/blob/main/%CE%91%CE%A3%CE%9A%CE%97%CE%A3%CE%97%201/image1.png)

**Εικόνα 1:** Η διαδικασία ταυτοποίησης γραμμικού χρονικά αμετάβλητου συστήματος.

Για τους σκοπούς αυτής της άσκησης θεωρούμε πως το άγνωστο σύστημα έχει (άγνωστη) πεπερασμένη κρουστική απόκριση h, δηλαδή μπορεί να μοντελοποιηθεί ως ένα FIR φίλτρο, όπως φαίνεται στην Εικόνα 1.

Επίσης, όπως απεικονίζεται στην Εικόνα 1, το σήμα εισόδου x(n)  (το οποίο θεωρήστε πως είναι λευκός Gaussian θόρυβος με μέση τιμή 0 και διασπορά 1 και πως αποτελείται από 1000 δείγματα) εισέρχεται παράλληλα στο άγνωστο σύστημα με συνάρτηση μεταφοράς H(z) , και στο FIR φίλτρο, με συνάρτηση μεταφοράς W(z) . Θεωρούμε ότι η έξοδος d(n) είναι άμεσα παρατηρήσιμη, χωρίς να μολύνεται από θόρυβο παρατήρησης.

Για τους πειραματικούς λόγους της παρούσας άσκησης θεωρήστε πως το άγνωστο σύστημα περιγράφεται από το FIR φίλτρο H(z), με συνάρτηση μεταφοράς

$$
H(z) = 1 - 0.4z^{-1} - 4z^{-2} + 0.5z^{-3}.
$$

Έτσι, η κρουστική απόκριση του υπό αναγνώριση συστήματος έχει την έκφραση,

$$
h(n) = \delta[n] - 0.4\delta[n - 1] - 4\delta[n - 2] + 0.5\delta[n - 3].
$$

Συνεπώς, η έξοδος του υπό αναγνώριση συστήματος θα εξαρτάται από την τρέχουσα τιμή του σήματος εισόδου καθώς και από ένα πεπερασμένο πλήθος παρελθοντικών τιμών του σήματος εισόδου, και πιο συγκεκριμένα θα δίνεται από την σχέση

$$
d(n) = x[n] - 0.4x[n - 1] - 4x[n - 2] + 0.5x[n - 3].
$$

Ομοίως θεωρούμε πως το FIR σύστημα \( W(z) \) έχει πεπερασμένη κρουστική απόκριση, η έξοδος του οποίου θα εξαρτάται από την τρέχουσα τιμή του σήματος εισόδου καθώς και από ένα πεπερασμένο πλήθος παρελθοντικών τιμών του σήματος εισόδου, δηλαδή

$$
y(n) = \sum_{k=0}^{L} w_n,_k x[n - k].
$$

Η τελευταία σχέση μπορεί να γραφεί ισοδύναμα ως ένα εσωτερικό διάνυσμα δύο διανυσμάτων, όπου το ένα διάνυσμα θα είναι το διάνυσμα των συντελεστών του FIR φίλτρου

$$
\mathbf{w}(n) = [w_0(n), w_1(n), \dots, w_L(n)],
$$

και το άλλο διάνυσμα θα περιέχει τα αντίστοιχα τρέχοντα δείγματα του σήματος εισόδου, δηλαδή

$$
\mathbf{x}(n) = [x(n), x(n - 1), \dots, x(n - L)].
$$

Συνεπώς η σχέση που δίνει την έξοδο του FIR φίλτρου είναι

$$
y(n) = \mathbf{w}(n)^T \mathbf{x}(n).
$$

**Ζητούμενα:**

### 1.1 (Θεωρητικό Ερώτημα)
Να διατυπωθεί θεωρητικά το βέλτιστο φίλτρο Wiener w(n).

### 1.2 (Πειραματικό Ερώτημα)
Υπολογίστε, με βάση τα δεδομένα, το φίλτρο Wiener  w(n), για την εκτίμηση των συντελεστών του H(z).

### 1.3 (Θεωρητικό Ερώτημα)
Κάνοντας εφαρμογή του αλγορίθμου LMS, προσπαθήστε να βρείτε ένα άνω φράγμα για την ποσότητα

$$
E[\mathbf{ŵ}(n)] = E[\mathbf{w}(n) - \mathbf{w}_0],
$$

όπου $$\mathbf{w}_0$$ είναι το βέλτιστο διάνυσμα συντελεστών, διασφαλίζοντας ταυτόχρονα ότι ο LMS αλγόριθμος συγκλίνει.

#### 1.3.1 (Θεωρητικό Ερώτημα)
Καθορίστε το διάστημα τιμών που δύναται να λαμβάνει το μέγεθος βήματος $$\mu$$ ώστε ο αλγόριθμος να συγκλίνει υπό την έννοια της μέσης τιμής.

#### 1.3.2 (Πειραματικό Ερώτημα)
Υλοποιήστε τον αλγόριθμο LMS. Χρησιμοποιείστε ένα φίλτρο w(n) με 4 συντελεστές. Αρχικοποιήστε το φίλτρο με μηδενική τιμή και χρησιμοποιήστε βήμα

$$
\mu = 0.1\mu_{\text{max}},
$$

όπου $$\mu_{\text{max}}$$ είναι το άνω φράγμα του βήματος για σύγκλιση ως προς τη μέση τιμή. Συγκρίνετε τους συντελεστές w(n)  με τους συντελεστές που προέκυψαν από το ερώτημα [1.2].

#### 1.3.3 (Πειραματικό Ερώτημα)
Πραγματοποιείστε τον αλγόριθμο LMS για τις πιθανές τιμές του βήματος

$$
\mu = [0.001\mu_{max},\ 0.01\mu_{max},\ 0.1\mu_{max},\ 0.5\mu_{max}].
$$

Τυπώστε την εξέλιξη των συντελεστών για κάθε περίπτωση.

##### 1.3.3.1 (Πειραματικό Ερώτημα)
Τυπώστε την καμπύλη μάθησης για τον αλγόριθμο LMS όταν το βήμα είναι $$\mu = 0.01$$ και το πλήθος των συντελεστών του FIR φίλτρου είναι 3 και 5. Τι παρατηρείτε;

## 2. Γραμμικό Χρονικά Μεταβαλλόμενο Σύστημα

Στο ερώτημα αυτό, μας ενδιαφέρει η περίπτωση στην οποία το σύστημα το οποίο επιθυμούμε να αναγνωρίσουμε είναι χρονικά μεταβαλλόμενο. Θα ασχοληθούμε με δύο διαφορετικές προσεγγίσεις. Στην πρώτη, θα πραγματοποιείται μία ομαλή μεταβολή του των συντελεστών του αγνώστου συστήματος, ενώ στην δεύτερη θα πραγματοποιείται μία πιο ακαριαία μεταβολή των συντελεστών του αγνώστου συστήματος.

![Εικόνα 2](https://github.com/nickpotamianos/STATISTIKI_EPEKSERGASIA_SIMATWN/blob/main/%CE%91%CE%A3%CE%9A%CE%97%CE%A3%CE%97%201/image2.png)

**Εικόνα 2:** Η διαδικασία ταυτοποίησης γραμμικού χρονικά μεταβαλλόμενου συστήματος.

Όπως απεικονίζεται στην Εικόνα 2, η μόνη διαφορά είναι πως τώρα έχουμε ένα χρονικά μεταβαλλόμενο σύστημα $$H_n(z)$$. Ας θεωρήσουμε πως το σύστημα αυτό έχει κρουστική απόκριση χρονικά μεταβαλλόμενη.

### 2.1 Ομαλή Μεταβολή

Αρχικά θεωρούμε πως η κρουστική απόκριση υφίσταται μία ομαλή χρονική μεταβολή με τον εξής τρόπο,

$$
h(n) = b(n)\delta[n] - 0.4\delta[n - 1] - 4\delta[n - 2] + 0.5\delta[n - 3],
$$

όπου b(n) είναι ένας χρονικά μεταβαλλόμενος συντελεστής που εξελίσσεται ως εξής,

$$
b(n) = \frac{1}{1 + e^{-0.02n}}, \quad n \in [1, 1000].
$$

### 2.2 Ακαριαία Μεταβολή

Στην συνέχεια θεωρούμε ότι η κρουστική απόκριση ακολουθεί μία πιο ακαριαία χρονική μεταβολή σύμφωνα με τον κανόνα:

$$
h(n) = b(n)\delta[n] - 0.4\delta[n - 1] - 4\delta[n - 2] + 0.5\delta[n - 3],
$$

όπου b(n) είναι ένας χρονικά μεταβαλλόμενος συντελεστής που εξελίσσεται ως εξής,

$$
b(n) =
\begin{cases}
100, & 1 \leq n \leq 500 \\
0, & 500 < n \leq 1000
\end{cases}.
$$

**Ζητούμενα:**

### 2.3 (Πειραματικό Ερώτημα)
Να σχεδιάσετε την καμπύλη μάθησης του αλγορίθμου LMS για κατάλληλη τιμή βήματος και για τις δύο πιθανές κρουστικές αποκρίσεις των ερωτημάτων [2.1] και [2.2].

### 2.4 (Πειραματικό Ερώτημα)
Να επαναλάβετε τις μετρήσεις για 20 διαφορετικές υλοποιήσεις του σήματος αναφοράς d(n). Για κάθε υλοποίηση, υπολογίστε το στιγμιαίο τετραγωνικό σφάλμα $$e^2(n)$$ συναρτήσει του n, και υπολογίστε το μέσο όρο του για όλες τις υλοποιήσεις.

## Διαδικαστικά

- **Μπορείτε να χρησιμοποιήσετε οποιαδήποτε γλώσσα προγραμματισμού επιθυμείτε.**
