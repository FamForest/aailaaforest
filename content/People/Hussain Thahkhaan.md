---
NID: Hussain Thahkhaan
ID:
Given Name: Hussain Thahkhaan
aliases:
DOB: 1928-12-31
DOD:
Status: Deceased
Gender: Male
Type: Person
Father: Sihthy Faan Husband
Mother: Sihthy Faan
Blood Group:
Spouse 1: "[[Khadheeja]]"
Spouse 1 Kids:
  - "[[People/Family/Noora Family/Hawwa & Sitti Mom/Sihthy Faan/Hussain Thakhkhaan/Wife 1/Mohamed Hussain/Mohamed Hussain|Mohamed Hussain]]"
  - "[[Hawwa Didi|Hawwa Didi]]"
Spouse 2 Kids:
  - "[[Aishath Hussain]]"
  - "[[Ali Hussain]]"
  - "[[Aminath Hussain]]"
  - "[[Hawwa Hussain]]"
  - "[[Khadheeja Hussain]]"
  - "[[Maryam Hussain]]"
  - "[[Zulaikha Hussain]]"
  - "[[Hassan Hussain]]"
Address:
  - "[[Blue Room, Hithadhoo, Addu City, Maldives]]"
tags:
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/SihthyFaan/HussainThahkhaan
  - Dhonbeefaan/SihthyFaan/HussainThahkhaan
Photo: https://lh3.googleusercontent.com/pw/AP1GczN6u2bzx_75xAADRB4OnqjDs6P3nJNCxfWHRhNWc6CVdLOgnRgUAVtUfMRqEEpTwNfUaRIgixQVic2tV04aWdNXuP_eISRHhCbjEqKk71lfLShl-OSL5BsaP6f-ngVpsFYhfMRWQYdVBy61Z2HZN1Wc=w767-h959-s-no?authuser=4
publish: true
---


# About `= this.file.name`

**Full Name:** `= this.file.name`
**Gender:** `= this.gender`
**Status:** `= choice(this.status, "Deceased", "Living")`
**Date of Birth:** `= this.dob`
**Date of Death:** `= this.dod` 
**Age at Death:** `= this.dod - this.dob`
**Current Age:** `= date(today) - this.dob`


# Family Relationships

## `= this.given-name`'s Parents & Grandparents
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Photo: image(Photo)
  Grand Mothers: |
    Mother.split(" (",1)
  Grand Fathers: |
    Father.split(" (",1)
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
      - file.name
      - DOB
      - DOD
      - formula.Grand Mothers
      - formula.Grand Fathers
    columnSize:
      file.name: 178
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 158
      formula.Grand Fathers: 110
  - type: table
    name: Parents Photo
    filters:
      or:
        - NID == this.Mother
        - NID == this.Father
    order:
      - formula.Photo
      - file.name
      - DOB
      - DOD
      - formula.Grand Mothers
      - formula.Grand Fathers
    columnSize:
      formula.Photo: 98
      file.name: 141
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 110
      formula.Grand Fathers: 110
    rowHeight: tall

```

## `= this.given-name`'s Children by Spouse(s)
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Spouse: if(this.Gender.isEmpty(),"Select Gender of the Person You're Viewing",if(this.gender.contains("Female"),Father.split(" (",1),Mother.split(" (",1)))
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
      - file.name
      - formula.Gender
      - DOB
      - formula.Spouse
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      file.name: 241
      formula.Gender: 90
      note.DOB: 115
  - type: table
    name: Children Photo
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
      formula.Photo: 98
      file.name: 199
      formula.Gender: 90
      note.DOB: 115
    rowHeight: tall

```

## `= this.given-name`'s Siblings & Half-siblings
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Gender: if(Gender.isEmpty(),"Sibling",if(gender.contains("Female"),"Sister","Brother"))
  Mother: Mother.split(" (",1)
  mother: mother.split(" (",1)
  Father: Father.split(" (",1)
  Photo: image(Photo)
properties:
  file.name:
    displayName: Sibling's Name
  formula.Father:
    displayName: Father
  formula.Mother:
    displayName: Mother
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
      - file.name
      - formula.Gender
      - DOB
      - formula.Mother
      - formula.Father
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      note.DOB: 112
      formula.Father: 139
      formula.Mother: 139
  - type: table
    name: Siblings and Half Siblings
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
      - formula.Mother
      - formula.Father
    sort:
      - property: Mother
        direction: ASC
    columnSize:
      formula.Photo: 98
      file.name: 160
      note.DOB: 112
      formula.Mother: 139
      formula.Father: 139
    rowHeight: tall

```
