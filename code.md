Let's go step by step to solve the questions.

### Question 1: 
```cpp
class Point2d {
public:
    double x, y;
};

class Triangle {
public:
    Point2d p1, p2, p3;

    double distance(const Point2d& p1, const Point2d& p2) {
        return sqrt((p2.x - p1.x)*(p2.x - p1.x) + (p2.y - p1.y)*(p2.y - p1.y));
    }

    double perimetre() {
        return distance(p1, p2) + distance(p2, p3) + distance(p1, p3);
    }
};
```
Tests:
```cpp
Point2d p1, p2, p3;
p1.x = 0, p1.y = 0;
p2.x = 1, p2.y = 0;
p3.x = 0, p3.y = 1;

Triangle t;
t.p1 = p1, t.p2 = p2, t.p3 = p3;

cout << "perimetre = " << t.perimetre() << endl;

Triangle& t2 = t;
t2.p1.x = 0, t2.p1.y = -1;

cout << "nouveau perimetre : " << t.perimetre() << endl << endl;
```

### Question 2:
```cpp
#include <string>

class Etudiant {
private:
    std::string nom;
    int ID;
    double moyenne;

public:
    Etudiant(std::string n, int id, double m) : nom(n), ID((id > 0) ? id : 1), moyenne((m >= 0 && m <= 20) ? m : 10) {}

    int get_ID() const {
        return ID;
    }

    void set_ID(int id) {
        if(id > 0)
            ID = id;
    }

    double get_moyenne() const {
        return moyenne;
    }

    void set_moyenne(double m) {
        if(m >= 0 && m <= 20)
            moyenne = m;
    }
};
```
### Question 3:
```cpp
class Promotion {
private:
    Etudiant* pE;
    int n;

public:
    Promotion(int nb) : n(nb) {
        pE = new Etudiant[n];
        for(int i=0; i<n; i++) {
            pE[i] = Etudiant("NON RENSEIGNE", 1, 10);
        }
    }

    Etudiant& operator[](int index) {
        return pE[index];
    }

    double moyenne() const {
        double sum = 0;
        for(int i=0; i<n; i++) {
            sum += pE[i].get_moyenne();
        }
        return sum / n;
    }

    ~Promotion() {
        delete[] pE;
    }
};
```

### Question 4:
Add `<` operator in `Etudiant` class and use STL sort function:
```cpp
#include <algorithm>

bool Etudiant::operator<(const Etudiant& E) const {
    return nom < E.nom;
}

//... (inside main function)

std::sort(promo.pE, promo.pE + M);
```

With these implementations, you can now use the provided test code to see the expected output.