---
NID: Aminath Manikfaan
ID:
First Name: Aminath
Last Name: Manikfaan
aliases:
  - Aminath Manikfaan
DOB:
DOD: 1979-08-02
Gender: Female
Father: Moosa Thahkhaan (Koshidhoragey)
Mother: Hawwa Faan
Spouse 1: "[[Hulhudhoo Ala Dhandigey Mohamed Manik]]"
Spouse 1 Kids:
  - "[[Fathmath Hilala]]"
Spouse 2: "[[Hoabeyyage Mohamed Didi|Mohamed Didi]]"
Spouse 2 Kids:
  - "[[Shaziyya Mohamed Didi|Shaziyya Mohamed Didi]]"
  - Aisa
  - Kahdha
Type: Person
tags:
  - Dhonbeefaan/HawwaFaan/AminathManikfaan
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/HawwaFaan/AminathManikfaan
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AminathManikfaan
Photo:
publish: true
---


# About `= this.first-name`

**ID:** `= this.id`
**Full Name:** `= this.first-name` `= this.last-name`
**Gender:** `= this.gender`
**Status:** `= choice(this.DOD, "Deceased", "Living")`
**Date of Birth:** `= this.dob`
**Date of Death:** `= this.dod` 
**Age at Death:** `= this.dod - this.dob`
**Current Age:** `= date(today) - this.dob`


# Family Relationships

## `= this.first-name` `= this.last-name`'s Parents & Grandparents
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Photo: image(Photo)
properties:
  note.Mother:
    displayName: Grand Mothers
  note.Father:
    displayName: Grand Fathers
  file.name:
    displayName: Parent's Name
views:
  - type: table
    name: Parents
    filters:
      or:
        - NID == this.Mother
        - NID == this.Father
    order:
      - formula.Photo
      - file.name
      - DOB
      - DOD
      - Father
      - Mother
    columnSize:
      formula.Photo: 99
      file.name: 141
      note.DOB: 105
      note.DOD: 105
      note.Father: 141
    rowHeight: tall

```

### `= this.first-name` `= this.last-name`'s Children by Spouse(s)
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Spouse: if(this.gender.contains("Female"),Father,Mother)
  Gender: if(Gender.isEmpty(),"Child",if(Gender.contains("Female"),"Daughter","Son"))
  Photo: image(Photo)
properties:
  file.name:
    displayName: Child's Name
views:
  - type: table
    name: Children
    filters:
      or:
        - Father == this.NID
        - Mother == this.NID
    order:
      - formula.Photo
      - file.name
      - formula.Gender
      - DOB
      - formula.Spouse
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      formula.Photo: 102
      file.name: 243
      note.DOB: 103
    rowHeight: tall

```

### `= this.first-name` `= this.last-name`'s Siblings & Half-siblings
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Gender: if(Gender.isEmpty(),"Sibling",if(gender.contains("Female"),"Sister","Brother"))
  Photo: image(Photo)
properties:
  file.name:
    displayName: Sibling's Name
views:
  - type: table
    name: Siblings & Half Siblings
    filters:
      and:
        - NID != this.NID
        - or:
            - Father == this.Father
            - Mother == this.Mother
    order:
      - formula.Photo
      - file.name
      - formula.Gender
      - DOB
      - Mother
      - Father
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      formula.Photo: 108
      file.name: 146
      note.DOB: 112
      note.Mother: 148
    rowHeight: tall

```
