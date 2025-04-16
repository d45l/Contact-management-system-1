#include <iostream> // Alleen iostream voor invoer/uitvoer

using namespace std;

const int MAX_CONTACTS = 100;

string namen[MAX_CONTACTS];
string telefoonnummers[MAX_CONTACTS];
int contactAantal = 0;

// Functie om een contact toe te voegen
void voegContactToe() {
    if (contactAantal < MAX_CONTACTS) {
        cout << "Voer naam in: ";
        cin.ignore();  // Voorkomt invoerproblemen
        getline(cin, namen[contactAantal]);
        cout << "Voer telefoonnummer in: ";
        getline(cin, telefoonnummers[contactAantal]);
        contactAantal++;
        cout << "Contact succesvol toegevoegd!\n";
    } else {
        cout << "Contactlijst is vol!\n";
    }
}

// Functie om alle contacten weer te geven
void toonContacten() {
    if (contactAantal == 0) {
        cout << "Geen contacten beschikbaar.\n";
        return;
    }
    cout << "\nContactlijst:\n";
    for (int i = 0; i < contactAantal; i++) {
        cout << i + 1 << ". " << namen[i] << " - " << telefoonnummers[i] << "\n";
    }
}

// Functie om een contact te zoeken op naam of telefoonnummer
void zoekContact() {
    if (contactAantal == 0) {
        cout << "Geen contacten beschikbaar om te zoeken.\n";
        return;
    }
    string zoekterm;
    cout << "Voer naam of telefoonnummer in om te zoeken: ";
    cin.ignore();
    getline(cin, zoekterm);
    bool gevonden = false;
    for (int i = 0; i < contactAantal; i++) {
        if (namen[i].find(zoekterm) != string::npos || telefoonnummers[i].find(zoekterm) != string::npos) {
            cout << "Gevonden: " << namen[i] << " - " << telefoonnummers[i] << "\n";
            gevonden = true;
        }
    }
    if (!gevonden) {
        cout << "Geen overeenkomst gevonden.\n";
    }
}

// Functie om een contact te verwijderen
void verwijderContact() {
    if (contactAantal == 0) {
        cout << "Geen contacten om te verwijderen.\n";
        return;
    }
    int index;
    cout << "Voer het nummer van het contact in om te verwijderen: ";
    cin >> index;
    if (index < 1 || index > contactAantal) {
        cout << "Ongeldig contactnummer!\n";
        return;
    }
    for (int i = index - 1; i < contactAantal - 1; i++) {
        namen[i] = namen[i + 1];
        telefoonnummers[i] = telefoonnummers[i + 1];
    }
    contactAantal--;
    cout << "Contact succesvol verwijderd!\n";
}

// Functie om een contact bij te werken
void updateContact() {
    if (contactAantal == 0) {
        cout << "Geen contacten om bij te werken.\n";
        return;
    }

    int index;
    cout << "Voer het nummer van het contact in dat je wilt bijwerken: ";
    cin >> index;
    if (index < 1 || index > contactAantal) {
        cout << "Ongeldig contactnummer!\n";
        return;
    }

    cin.ignore();  // Voor correcte invoer na cin >>

    cout << "Huidige naam: " << namen[index - 1] << "\n";
    cout << "Nieuwe naam (druk op Enter om niet te wijzigen): ";
    string nieuweNaam;
    getline(cin, nieuweNaam);
    if (!nieuweNaam.empty()) {
        namen[index - 1] = nieuweNaam;
    }

    cout << "Huidig telefoonnummer: " << telefoonnummers[index - 1] << "\n";
    cout << "Nieuw telefoonnummer (druk op Enter om niet te wijzigen): ";
    string nieuwNummer;
    getline(cin, nieuwNummer);
    if (!nieuwNummer.empty()) {
        telefoonnummers[index - 1] = nieuwNummer;
    }

    cout << "Contact bijgewerkt!\n";
}
// Hoofdprogramma
int main() {
    int keuze;
    do {
        cout << "\nContactbeheer Systeem\n";
        cout << "1. Contact toevoegen\n";
        cout << "2. Contacten bekijken\n";
        cout << "3. Contact zoeken\n";
        cout << "4. Contact verwijderen\n";
        cout << "5. Afsluiten\n";
        cout << "Voer uw keuze in: ";
        cout << "6. Contact bijwerken\n";
        cin >> keuze;
        
        if (keuze == 1) {
            voegContactToe();
        } else if (keuze == 2) {
            toonContacten();
        } else if (keuze == 3) {
            zoekContact();
        } else if (keuze == 4) {
            verwijderContact();
        } else if (keuze == 5) {
            cout << "Afsluiten...\n";
        } else {
            cout << "Ongeldige keuze! Probeer opnieuw.\n";
        }
        
    } while (keuze != 5);
    
    return 0;
}
