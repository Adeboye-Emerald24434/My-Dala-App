# My Dala App — Responsive Correction Notes

## How to use this version

Keep your original project open beside this corrected project.

Do not just copy the CSS blindly. Compare one section at a time and ask:

> "What was my original code telling the browser to do, and what is the corrected code telling it to do?"

## 1. Fixed widths vs flexible widths

### Original
```css
.search-input {
    width: 400px;
}
```

### Corrected
```css
.search-form {
    width: 400px;
    max-width: 100%;
}

.search-box {
    width: 100%;
}
```

A 400px search box can be wider than a small phone. `max-width: 100%` prevents it from becoming wider than its available space.

Also, the form and the input now have different classes. One class should not be responsible for two different elements with two different jobs.

---

## 2. Fixed margins were causing overflow

### Original
```css
.button {
    margin-left: 150px;
}
```

### Corrected
```css
.button {
    width: min(90%, 1200px);
    margin: 20px auto;
}
```

`margin-left: 150px` works around a particular desktop position. It does not adapt well when the screen becomes smaller.

`margin: auto` lets the browser center the element.

`min(90%, 1200px)` means:
- use 90% of the available width
- but never become wider than 1200px

---

## 3. Flexbox should be allowed to wrap

### Original
```css
.card-child {
    display: flex;
}

.card-item {
    width: 25%;
}
```

That forces four cards into one row.

### Corrected
```css
.card-child {
    display: flex;
    flex-wrap: wrap;
}

.card-item {
    flex: 1 1 200px;
}
```

The cards can now move to another row when there isn't enough room.

This is one of the most important responsive-design ideas.

---

## 4. Compare page

### Original
```css
.form-selection {
    display: flex;
}

.select-1 {
    width: 30%;
}
```

On a desktop this creates three columns.

On a phone, three columns can become cramped.

### Corrected
```css
.form-selection {
    display: flex;
    flex-wrap: wrap;
}

@media (max-width: 767.98px) {
    .form-selection {
        flex-direction: column;
    }

    .select-1 {
        width: 100%;
    }
}
```

Desktop:
```text
[ Item ] [ City A ] [ City B ]
```

Mobile:
```text
[ Item ]

[ City A ]

[ City B ]
```

---

## 5. Report form height

### Original
```css
.container-f {
    height: 350px;
}
```

A fixed height can become a problem when content needs more vertical space.

### Corrected
```css
.container-f {
    min-height: 350px;
    height: auto;
}
```

The form can now grow when necessary.

---

## 6. Report form fields

### Original
```css
.half-input {
    display: flex;
}
```

### Corrected on mobile
```css
@media (max-width: 767.98px) {
    .half-input {
        flex-direction: column;
    }
}
```

Desktop:
```text
Market                 City
[.............]        [.............]
```

Mobile:
```text
Market
[....................]

City
[....................]
```

---

## 7. Profile cards

### Original
```css
.green-card {
    width: 40%;
}

.white-card {
    width: 40%;
}
```

### Corrected
```css
.green-card,
.white-card {
    width: min(90%, 600px);
}
```

This keeps the cards readable on desktop while allowing them to use most of the screen on a phone.

---

## 8. Images

The corrected project also adds:

```css
img {
    max-width: 100%;
    height: auto;
}
```

This prevents images from forcing their parent/container wider than the screen.

---

## 9. box-sizing

The original project already had this on some pages, but not consistently.

The corrected version uses:

```css
* {
    box-sizing: border-box;
}
```

This makes width calculations easier because padding and borders are included in the declared width.

---

## 10. Bootstrap versions

Some pages used Bootstrap 5.0.2 CSS while loading Bootstrap 5.3.8 JavaScript.

The corrected project uses Bootstrap 5.3.8 for both.

---

## 11. CSS mistakes corrected

Examples:

### Invalid
```css
flex: wrap;
```

### Correct
```css
flex-wrap: wrap;
```

The malformed `}-badge` selector was also removed.

Invalid/incomplete `box-shadow` declarations were removed rather than pretending they were valid shadows.

---

## 12. A responsive-design checklist

Before you submit your next project, check:

- [ ] Is there a viewport meta tag?
- [ ] Am I using unnecessary fixed widths?
- [ ] Am I using large fixed left/right margins?
- [ ] Can my flex items wrap?
- [ ] What happens to my columns on a phone?
- [ ] Can images overflow their containers?
- [ ] Do forms stack on small screens?
- [ ] Are buttons still usable on a phone?
- [ ] Does text remain readable?
- [ ] Does horizontal scrolling appear?
- [ ] Have I tested around 320px–390px wide?
- [ ] Have I tested tablet width?
- [ ] Have I tested desktop width?

## The main idea

Responsive design is not simply:

```css
@media (...) {
    /* make things smaller */
}
```

It starts with building a layout that can naturally grow, shrink and wrap.

Think about:

```text
Desktop → more space → row layout

Tablet → less space → fewer columns

Mobile → very little space → stacked layout
```

That is the mindset I want you to take from this correction.
