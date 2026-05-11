# EduManage — CONTEXT.md
# School Domain Language

This file extends ansai-core/CONTEXT.md with terms
specific to the EduManage product line.
All global terms defined in ansai-core/CONTEXT.md apply.
This file adds school-specific domain language.

One meaning per term. Locally enforced.
When a global term and a local term appear to conflict —
the global definition governs.

---

## School Structure Terms

**School DNA**
The foundational configuration of a school that cascades
into all downstream modules.
Four dimensions: schoolType, schoolGender,
schoolLevel, schoolCategory.
Derived through deriveSchoolConfig() utility.
Every module reads School DNA before rendering.

**schoolType**
Whether the school is day, boarding, or day-and-boarding.
Determines: dormitory modules, meals, transport relevance.

**schoolGender**
Whether the school is boys-only, girls-only, or mixed.
Determines: available roles, dormitory configuration,
sports and activities modules.

**schoolLevel**
Whether the school is junior secondary, senior secondary,
or both. Determines: curriculum modules, exam types,
CBC vs 844 applicability.

**schoolCategory**
Whether the school is national, extra-county, county,
sub-county, or private. Determines: fee structures,
government reporting requirements, admission modules.

**TRANSITION level**
The majority Kenyan secondary school case for 2026.
Schools running both CBC and 844 simultaneously as
Kenya transitions between curriculum systems.
EduManage handles both. TRANSITION is the default
assumption until the school's DNA specifies otherwise.

---

## Curriculum Terms

**CBC — Competency Based Curriculum**
Kenya's current curriculum framework replacing 844.
Eight-level grading scale. SBA tracking.
No ranking enforcement (KNEC requirement).
KNEC CBA export readiness required.

**844**
Kenya's previous curriculum framework.
8-4-4: 8 years primary, 4 years secondary, 4 years university.
Still active in TRANSITION schools.

**SBA — School Based Assessment**
Continuous assessment component of CBC.
Tracked per student per subject per term.
Must be exportable in KNEC CBA format.

**KNEC**
Kenya National Examinations Council.
The regulatory body for national examinations.
EduManage must be KNEC CBA export-ready at all times.

**Form**
The year level in a Kenyan secondary school.
Form 1 through Form 4 (844).
Grade 7 through Grade 9 (CBC junior secondary).
Grade 10 through Grade 12 (CBC senior secondary).

**Stream**
A parallel class within the same form.
Form 2A, Form 2B, Form 2C — three streams of Form 2.
Each stream has its own class teacher.

---

## People Terms

**Principal**
The head of a school institution.
Highest authority role within the tenant.
Has access to all modules.
Role code: PRINCIPAL.

**Deputy Principal**
Second in command. Typically manages academic affairs
or administration depending on school structure.
Role code: DEPUTY_PRINCIPAL.

**HOD — Head of Department**
Subject department leader.
Manages teachers within their subject area.
Role code: HOD.

**Class Teacher**
The teacher assigned pastoral responsibility
for a specific class (form and stream).
Different from subject teacher.
Role code: CLASS_TEACHER.

**Bursar**
The school's financial officer.
Manages fee collection, payments, and financial records.
The person who uses the fee management module most.
The named human being behind every financial feature.
Role code: BURSAR.

**Patron / Matron**
Staff member responsible for boarding students.
Patron for boys. Matron for girls.
Role code: PATRON / MATRON.

**Parent / Guardian**
The adult with parental responsibility for a student.
Has access to the parent portal only.
Can view their child's records. Cannot edit.
Role code: PARENT.

**Student**
The person the entire system exists to serve.
Has limited direct system access.
Their data is what the system exists to protect.
Role code: STUDENT.

---

## Financial Terms

**Fee structure**
The complete schedule of fees a school charges.
Varies by schoolCategory, schoolGender, schoolLevel,
boarding status, and term.
Configured in School DNA. Applied to all students.

**Fee balance**
The amount a student owes after payments are applied.
Can be positive (owes money), zero (fully paid),
or negative (overpaid — credit applied to next term).

**Term**
The three academic periods of a Kenyan school year.
Term 1: January to April.
Term 2: May to August.
Term 3: September to November.
Fee billing aligns with term start dates.

**Invoice**
A formal fee statement generated per student per term.
Contains: fee structure breakdown, previous balance,
payments received, amount due.

**Receipt**
Proof of payment issued when a fee payment is recorded.
Contains: student name, amount paid, date, balance remaining,
payment method, bursar who recorded it.
Every receipt has an audit trail.

**M-PESA**
Kenya's mobile money platform.
The primary fee payment method for most schools.
Daraja API integration for direct school payment collection.
Callbacks must be hardened — see security baseline.

---

## Operational Terms

**Admission**
The process of enrolling a new student into the school.
Captures: personal details, parent/guardian details,
previous school, admission number, form, stream.
Generates the student's permanent record.

**Admission number**
The unique identifier assigned to a student
by the school on admission.
Not the same as the system ID.
Used in all official school communications.

**School visiting day**
A scheduled day when parents visit the school.
Relevant to the parent portal — notifications,
reports, and fee statements are often timed
around visiting days.

**Closing day**
The last day of a school term.
Triggers: end-of-term report generation,
fee balance summaries, next term fee invoices.

**Opening day**
The first day of a school term.
Triggers: new term fee billing,
attendance module reset, new stream assignments.

---

## Technical Terms Specific to EduManage

**school_id**
The tenant identifier in EduManage.
Every database table has this column.
Every query must include WHERE school_id = ?
enforced at the tenantGuard middleware level.
Missing school_id scoping is a gross violation.

**tenantGuard**
The middleware that enforces school_id scoping
on every incoming request.
Lives in @ansai/tenancy.
No request reaches a route handler without
passing through tenantGuard.

**deriveSchoolConfig()**
The utility function that reads a school's DNA
and returns the configuration object used
by all downstream modules.
Called once per session. Cached per request.
Never bypassed.

---

## Amendment Record

Changes to this document follow Category 1 governance
for new term additions and Category 2 governance for
redefining existing school domain terms.
All amendments logged in ansai-core/AMENDMENTS.md.
