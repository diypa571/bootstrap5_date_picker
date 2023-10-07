Datepicker med Bootstrap 5
Detta projekt demonstrerar hur man integrerar biblioteket vanillajs-datepicker med Bootstrap 5 för att skapa en interaktiv datumväljare, där tidigare datum är inaktiverade.

// Funktion för att hämta titeln för datumväljaren, antingen från nästa <label>-element eller från 'aria-label'-attributet.
const theDatePicker = elem => {
    const label = elem.nextElementSibling;  // Hämta nästa syskonelement till elem
    let theTitle = '';  // Initiera en variabel för titeln

    // Kontrollera om nästa syskonelement är en <label>
    if (label && label.tagName === 'LABEL') {
        theTitle = label.textContent;  // Använd textinnehållet i <label> som titel
    } else {
        // Använd 'aria-label'-attributet som titel, eller använd en tom sträng om det inte finns något 'aria-label'
        theTitle = elem.getAttribute('aria-label') || '';
    }
    return theTitle;  // Returnera titeln
};

// Skapa ett datumobjekt för "idag" och ställ in tiden till midnatt
const today = new Date();
today.setHours(0, 0, 0, 0);  

// Hämta alla input-element med klassen 'datepicker_input'
const ElemInput = document.querySelectorAll('.datepicker_input');

// Iterera över alla hämtade input-element
for (const elem of ElemInput) {
    // Skapa en ny datumväljare för aktuellt input-element
    const datepicker = new Datepicker(elem, {
        'format': 'yyyy-mm-dd',  // Formatet som datumet ska visas i
        title: theDatePicker(elem),  // Sätt titeln med hjälp av funktionen ovan
        minDate: today  // Inaktivera alla datum före dagens datum
    });

    // Lägg till en händelselyssnare till input-elementet som gömmer datumväljaren när ett datum har valts
    elem.addEventListener('changeDate', () => {
        datepicker.hide();
    });
}
