---
Name: Noora Mohamed
ID: "[[Noora Mohamed (b. 1996)]]"
First Name:
Given Name: Noora
Last Name: Mohamed
aliases:
DOB: 1996-08-01
DOD:
Status:
Gender: Female
Type: Person
Father: "[[Mohamed Hussain (1951-2005)]]"
Mother: "[[Safiyya Hussain (b. 1964)]]"
Spouse 1: "[[Mohamed Sameeh (b. 1997)]]"
Address:
  - "[[Likagasdhoshuge, Hithadhoo, Addu City, Maldives]]"
Photo:
dg-publish: false
dg-home:
Spouse 1 Kids:
tags:
---
# About `= this.given-name`

```dataviewjs
const p = dv.current();

// Retrieve fields
const firstName = p["first-name"];
const givenName = p["given-name"];
const lastName = p["last-name"];
const aliases = p.aliases;

// Collect non‑empty name parts
const nameParts = [];
if (firstName) nameParts.push(firstName);
if (givenName) nameParts.push(givenName);
if (lastName) nameParts.push(lastName);

// Build the base name (space‑joined)
let name = nameParts.join(" ");

// Add aliases in parentheses if present
if (aliases) {
    name += ` (${aliases})`;
}

// Output with "**Full Name:**" label
dv.span(`**Full Name:** ${name}`);
```
**Gender:** `= this.gender`
```dataviewjs
const p = dv.current();
const today = new Date();


if (p.status) {
    dv.span("**Status:** Passed away");
} else if (p.dod) {
    const deathDate = dv.date(p.dod);
    const yearsSince = Math.floor((today - deathDate) / (1000 * 60 * 60 * 24 * 365.25));
    let ageText = "";
    if (p.dob) {
        const birthDate = dv.date(p.dob);
        const ageAtDeath = Math.floor((deathDate - birthDate) / (1000 * 60 * 60 * 24 * 365.25));
        ageText = `, at age ${ageAtDeath}`;
    }
    dv.span(`**Status:** Passed away ${yearsSince} years ago${ageText}`);
} else if (p.dob) {
    const birthDate = dv.date(p.dob);
    const currentAge = Math.floor((today - birthDate) / (1000 * 60 * 60 * 24 * 365.25));
    dv.span(`**Current Age:** ${currentAge} Years`);
} else {

}
```

---
# `= this.given-name`'s Parents: 
```dataviewjs
const page = dv.current();
const givenName = page["given-name"];

// ---------- Clean wikilink (removes (b. ), (d. ), (YYYY-YYYY)) ----------
function toCleanWikilink(value) {
    if (value == null) return null;
    
    function basename(path) {
        return path.split('/').pop().replace(/\.md$/, '');
    }
    
    function removeYearInfo(str) {
        // Removes (b. YYYY), (d. YYYY), (YYYY-YYYY) and (YYYY–YYYY)
        return str.replace(/\s*\((?:b\.|d\.)\s*\d{4}(?:[-–]\d{4})?\)|\s*\(\d{4}[-–]\d{4}\)\s*/gi, '').trim();
    }
    
    if (value.path !== undefined) {
        const fullPath = value.path;
        const target = basename(fullPath);
        const display = removeYearInfo(target);
        return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
    }
    
    if (typeof value === "string") {
        const wikiMatch = value.match(/^\[\[(.*?)\]\]$/);
        if (wikiMatch) {
            let inner = wikiMatch[1];
            if (inner.includes('|')) {
                let [target, alias] = inner.split('|');
                const cleanedAlias = removeYearInfo(alias);
                return `[[${target}|${cleanedAlias}]]`;
            } else {
                const target = inner;
                const display = removeYearInfo(target);
                return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
            }
        }
        return removeYearInfo(value);
    }
    
    if (Array.isArray(value) && value.length > 0) {
        return toCleanWikilink(value[0]);
    }
    
    return null;
}

// ---------- Helper: get page object from a link field ----------
function getLinkedPage(field) {
    if (!field) return null;
    let path = null;
    if (field.path !== undefined) {
        path = field.path;
    } else if (typeof field === 'string') {
        const match = field.match(/^\[\[(.*?)(?:\|.*)?\]\]$/);
        if (match) {
            path = match[1];
        }
    }
    if (path) {
        if (!path.endsWith('.md')) path = path + '.md';
        return dv.page(path);
    }
    return null;
}

// ---------- Helper: output parent + grandparents ----------
function outputParentAndGrandparents(parentField, parentLabel, grandparentLabel, grandparentTag) {
    if (!parentField) return;
    
    // Output parent heading
    const parentDisplay = toCleanWikilink(parentField);
    if (parentDisplay) {
        if (givenName) {
            dv.span(`#### ${givenName}'s ${parentLabel} is ${parentDisplay}`);
        } else {
            dv.span(`#### ${parentLabel} is ${parentDisplay}`);
        }
    }

    // Find parent's page and show grandparents
    const parentPage = getLinkedPage(parentField);
    if (parentPage) {
        let lines = [];
        
        const grandmother = parentPage.Mother;
        if (grandmother) {
            const cleaned = toCleanWikilink(grandmother);
            if (cleaned) lines.push(`> **${grandparentLabel} Grandmother:** ${cleaned}`);
        }
        
        const grandfather = parentPage.Father;
        if (grandfather) {
            const cleaned = toCleanWikilink(grandfather);
            if (cleaned) lines.push(`> **${grandparentLabel} Grandfather:** ${cleaned}`);
        }
        
        if (lines.length > 0) {
            dv.paragraph(lines.join('\n'));
        }
    }
}

// ---------- Output Mother and Father ----------
outputParentAndGrandparents(page.Mother, "Mother", "Maternal", "Maternal");
outputParentAndGrandparents(page.Father, "Father", "Paternal", "Paternal");
```

---
# `= this.given-name`'s Spouse(s) & Children: 
```dataviewjs
const page = dv.current();
const givenName = page["given-name"];

// ---------- Clean wikilink (removes (b. ), (d. ), (YYYY-YYYY)) ----------
function toCleanWikilink(value) {
    if (value == null) return null;
    
    function basename(path) {
        return path.split('/').pop().replace(/\.md$/, '');
    }
    
    function removeYearInfo(str) {
        return str.replace(/\s*\((?:b\.|d\.)\s*\d{4}(?:[-–]\d{4})?\)|\s*\(\d{4}[-–]\d{4}\)\s*/gi, '').trim();
    }
    
    if (value.path !== undefined) {
        const fullPath = value.path;
        const target = basename(fullPath);
        const display = removeYearInfo(target);
        return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
    }
    
    if (typeof value === "string") {
        const wikiMatch = value.match(/^\[\[(.*?)\]\]$/);
        if (wikiMatch) {
            let inner = wikiMatch[1];
            if (inner.includes('|')) {
                let [target, alias] = inner.split('|');
                const cleanedAlias = removeYearInfo(alias);
                return `[[${target}|${cleanedAlias}]]`;
            } else {
                const target = inner;
                const display = removeYearInfo(target);
                return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
            }
        }
        return removeYearInfo(value);
    }
    
    if (Array.isArray(value) && value.length > 0) {
        return toCleanWikilink(value[0]);
    }
    
    return null;
}

// ---------- Helper: get raw string for ID matching ----------
function getRawString(field) {
    if (!field) return null;
    if (typeof field === 'string') return field;
    if (typeof field === 'object' && field.path) {
        const fileName = field.path.replace(/\.md$/, '');
        return `[[${fileName}]]`;
    }
    return String(field);
}

// ---------- Process each spouse ----------
let spouseIndex = 1;
while (true) {
    const spouseField = page[`Spouse ${spouseIndex}`];
    if (!spouseField) break;

    const verb = spouseIndex === 1 ? "married" : "also married";

    const spouseDisplay = toCleanWikilink(spouseField);
    if (spouseDisplay) {
        if (givenName) {
            dv.span(`#### ${givenName} ${verb} ${spouseDisplay}`);
        } else {
            dv.span(`#### ${verb.charAt(0).toUpperCase() + verb.slice(1)} ${spouseDisplay}`);
        }
    }

    const spouseRaw = getRawString(spouseField);
    const currentID = getRawString(page.ID);
    const gender = page.Gender;

    if (currentID && spouseRaw) {
        let childrenSet = new Set();

        let matchedPages = [];
        if (gender === "Female") {
            matchedPages = dv.pages().where(p =>
                getRawString(p.Mother) === currentID &&
                getRawString(p.Father) === spouseRaw
            );
        } else if (gender === "Male") {
            matchedPages = dv.pages().where(p =>
                getRawString(p.Father) === currentID &&
                getRawString(p.Mother) === spouseRaw
            );
        }
        for (let child of matchedPages) {
            const childLink = child.file.link;
            if (childLink) {
                const cleaned = toCleanWikilink(childLink);
                if (cleaned) childrenSet.add(cleaned);
            }
        }

        const spouseKids = page[`Spouse ${spouseIndex} Kids`];
        if (spouseKids && Array.isArray(spouseKids)) {
            for (let kid of spouseKids) {
                const cleaned = toCleanWikilink(kid);
                if (cleaned) childrenSet.add(cleaned);
            }
        }

        if (childrenSet.size > 0) {
            let quote = `> **Children from this marriage:**\n`;
            for (let childStr of childrenSet) {
                quote += `> - ${childStr}\n`;
            }
            dv.paragraph(quote);
        }
    }

    spouseIndex++;
}
```

---
# `= this.given-name`'s Siblings & Half Siblings

```dataviewjs
// ---------- Clean wikilink (removes (b. ), (d. ), (YYYY-YYYY)) ----------
function toCleanWikilink(value) {
    if (value == null) return null;
    
    function basename(path) {
        return path.split('/').pop().replace(/\.md$/, '');
    }
    
    function removeYearInfo(str) {
        // Removes (b. YYYY), (d. YYYY), (YYYY-YYYY) and (YYYY–YYYY)
        return str.replace(/\s*\((?:b\.|d\.)\s*\d{4}(?:[-–]\d{4})?\)|\s*\(\d{4}[-–]\d{4}\)\s*/gi, '').trim();
    }
    
    if (value.path !== undefined) {
        const fullPath = value.path;
        const target = basename(fullPath);
        const display = removeYearInfo(target);
        return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
    }
    
    if (typeof value === "string") {
        const wikiMatch = value.match(/^\[\[(.*?)\]\]$/);
        if (wikiMatch) {
            let inner = wikiMatch[1];
            if (inner.includes('|')) {
                let [target, alias] = inner.split('|');
                const cleanedAlias = removeYearInfo(alias);
                return `[[${target}|${cleanedAlias}]]`;
            } else {
                const target = inner;
                const display = removeYearInfo(target);
                return display === target ? `[[${target}]]` : `[[${target}|${display}]]`;
            }
        }
        return removeYearInfo(value);
    }
    
    if (Array.isArray(value) && value.length > 0) {
        return toCleanWikilink(value[0]);
    }
    
    return null;
}

// Helper: get a comparable identifier from a Link object or string (for matching, no cleaning)
function getLinkId(value) {
    if (!value) return null;
    if (value.path !== undefined) return value.path;
    if (typeof value === 'string') {
        const match = value.match(/\[\[(.*?)\]\]/);
        return match ? match[1] : value;
    }
    return value.toString();
}

const current = dv.current();

const currentMotherId = getLinkId(current.Mother);
const currentFatherId = getLinkId(current.Father);
const currentId = getLinkId(current.ID);

if (!currentMotherId || !currentFatherId || !currentId) {
    dv.paragraph("⚠️ This note needs `Mother`, `Father`, and `ID` fields (as internal links) to show siblings.");
} else {
    const allPeople = dv.pages('""')
        .where(p => {
            if (p.Type !== "Person") return false;
            if (p.file.folder?.includes("_Templates")) return false;
            const pId = getLinkId(p.ID);
            if (pId === currentId) return false;
            const pMother = getLinkId(p.Mother);
            const pFather = getLinkId(p.Father);
            return (pMother === currentMotherId || pFather === currentFatherId);
        });

    const rows = [];
    for (let p of allPeople) {
        const pMother = getLinkId(p.Mother);
        const pFather = getLinkId(p.Father);
        let relation = "";

        if (pMother === currentMotherId && pFather === currentFatherId) {
            if (p.Gender === "Female") relation = "Sister";
            else if (p.Gender === "Male") relation = "Brother";
            else relation = "Sibling";
        }
        else if (pMother === currentMotherId) {
            if (p.Gender === "Female") relation = "Maternal Half‑Sister";
            else if (p.Gender === "Male") relation = "Maternal Half‑Brother";
            else relation = "Maternal Half‑Sibling";
        }
        else if (pFather === currentFatherId) {
            if (p.Gender === "Female") relation = "Paternal Half‑Sister";
            else if (p.Gender === "Male") relation = "Paternal Half‑Brother";
            else relation = "Paternal Half‑Sibling";
        }
        else {
            relation = "Unknown";
        }

        // Clean the sibling link (removes year info)
        const cleanedSibling = toCleanWikilink(p.file.link);
        // Clean the mother and father fields
        const cleanedMother = p.Mother ? toCleanWikilink(p.Mother) : "—";
        const cleanedFather = p.Father ? toCleanWikilink(p.Father) : "—";

        rows.push({
            sibling: cleanedSibling,
            relation: relation,
            mother: cleanedMother,
            father: cleanedFather,
            dob: p.DOB ? dv.date(p.DOB) : null
        });
    }

    rows.sort((a, b) => {
        if (!a.dob && !b.dob) return 0;
        if (!a.dob) return 1;
        if (!b.dob) return -1;
        return a.dob.valueOf() - b.dob.valueOf();
    });

    if (rows.length === 0) {
        dv.paragraph("*No siblings found.*");
    } else {
        dv.table(
            ["Sibling", "Relation", "Mother", "Father"],
            rows.map(r => [r.sibling, r.relation, r.mother, r.father])
        );
    }
}
```

---
# `= this.given-name`'s Distinct Ancestral Lines
```dataviewjs
const current = dv.current();

// ---------- Helpers ----------
function getRawString(field) {
    if (!field) return null;
    if (typeof field === 'string') return field;
    if (typeof field === 'object' && field.path !== undefined) {
        return `[[${field.path.replace(/\.md$/, '')}]]`;
    }
    return String(field);
}

function getPageFromLink(linkField) {
    let raw = getRawString(linkField);
    if (!raw) return null;
    let match = raw.match(/\[\[(.*?)\]\]/);
    let target = match ? match[1] : raw;
    return dv.page(target);
}

function getAlias(page) {
    if (!page) return null;
    return page["Given Name"] || page.file.name;
}

function formatLink(page, isMe = false) {
    if (!page) return '?';
    const alias = getAlias(page);
    const target = page.file.path.replace(/\.md$/, '');
    const displayAlias = isMe ? alias : `${alias} ge`;
    const link = `[[${target}|${displayAlias}]]`;
    if (isMe) return `**${link}**`;
    return `*${link}*`;
}

// Recursively build all ancestor paths (depth 1 = parent, up to maxDepth)
function collectPaths(person, currentDepth, maxDepth, currentPath, allPaths) {
    if (!person) return;
    if (currentDepth > maxDepth) {
        allPaths.push([...currentPath]);
        return;
    }
    let hasParent = false;
    if (person.Mother) {
        const motherPage = getPageFromLink(person.Mother);
        if (motherPage) {
            hasParent = true;
            currentPath.push(motherPage);
            collectPaths(motherPage, currentDepth + 1, maxDepth, currentPath, allPaths);
            currentPath.pop();
        }
    }
    if (person.Father) {
        const fatherPage = getPageFromLink(person.Father);
        if (fatherPage) {
            hasParent = true;
            currentPath.push(fatherPage);
            collectPaths(fatherPage, currentDepth + 1, maxDepth, currentPath, allPaths);
            currentPath.pop();
        }
    }
    if (!hasParent && currentDepth <= maxDepth) {
        // End of line – store whatever path we have
        allPaths.push([...currentPath]);
    }
}

// ---------- Main ----------
if (!current) {
    dv.paragraph("No current file.");
} else {
    const MAX_DEPTH = 100;
    const allPaths = [];
    collectPaths(current, 1, MAX_DEPTH, [], allPaths);

    if (allPaths.length === 0) {
        dv.paragraph("No ancestors found. Add Mother and Father fields.");
    } else {
        let output = "";

        // --- 1. Unique furthest ancestors as BOLD numbered list ---
        const furthestSet = new Set();
        for (let path of allPaths) {
            if (path.length > 0) {
                const furthest = path[path.length - 1];
                furthestSet.add(furthest.file.path);
            }
        }

        if (furthestSet.size > 0) {
            output += `### Furthest Ancestors\n`;
            let idx = 1;
            for (let filePath of furthestSet) {
                const page = dv.pages().find(p => p.file.path === filePath);
                if (page) {
                    const alias = getAlias(page);
                    const target = page.file.path.replace(/\.md$/, '');
                    const boldLink = `**[[${target}|${alias}]]**`;
                    output += `${idx}. ${boldLink}\n`;
                    idx++;
                }
            }
            output += `\n`;
        } else {
            output += `*No ancestors found.*\n\n`;
        }

        // --- 2. All ancestral chains as a numbered list (unchanged) ---
        output += `### Ancestral Chains\n`;
        let chainNumber = 1;
        for (let path of allPaths) {
            const reversedPath = [...path].reverse();
            const items = [];
            for (let anc of reversedPath) {
                items.push(formatLink(anc, false));
            }
            items.push(formatLink(current, true));
            output += `${chainNumber}. ${items.join(', ')}\n`;
            chainNumber++;
        }

        dv.paragraph(output);
    }
}
```

