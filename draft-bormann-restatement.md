---
v: 3

title: The Restatement Anti-Pattern
abbrev: The Restatement Anti-Pattern
docname: draft-bormann-restatement-latest
category: info
stream: independent

date:
consensus:
area:
workgroup:
keyword:

venue:
  mail: "ietf@ietf.org"
  github: "cabo/restatement"

author:
  -
    ins: C. Bormann
    name: Carsten Bormann
    org: Universität Bremen TZI
    street: Postfach 330440
    city: Bremen
    code: D-28359
    country: Germany
    phone: +49-421-218-63921
    email: cabo@tzi.org

informative:
  KOENIG:
    author:
      name: Andrew Koenig
    title: Patterns and Antipatterns
    seriesinfo:
      J. Object Oriented Program.: >
        8(1): pp. 46-48
    date: 1995
  ANTIPATTERN:
    target: http://wiki.c2.com/?AntiPattern
    title: Anti Pattern
    rc: C2 Wiki (Last edited:)
    date: 2012-11-21
  WP-ANTIPATTERN:
    target: https://en.wikipedia.org/w/index.php?title=Anti-pattern&oldid=1144938932
    title: Anti-pattern
    rc: Wikipedia page (at the time of writing:)
    date: 2023-07-21
  RFC3552: seccons
  RFC2397:
  errata2397:
    target: https://www.rfc-editor.org/errata/rfc2397
    title: "RFC Errata Report » RFC Editor"
    rc: search result
  RFC9399:
# Examples:
  RFC5988:
  RFC6690:
  RFC8288:
  RFC7230:
  RFC4648:
  RFC7515:
  RFC6991:
  I-D.ietf-netmod-rfc6991-bis:
  RFC3339:
  I-D.ietf-sedate-datetime-extended:
  I-D.draft-ietf-rats-eat-20:
  rats-comment:
    target: https://mailarchive.ietf.org/arch/msg/rats/H8qXwQywD0W6x4QcC9Iwd5LYl2s
    title: >
      Re: [Rats] I-D Action: draft-ietf-rats-eat-20.txt
    author:
      name: Carsten Bormann
  RFC8555:
  I-D.draft-ietf-acme-subdomains-04:
  acme-comment:
    date: 2022-11-23
    target: https://mailarchive.ietf.org/arch/msg/last-call/v0RYQkByhAII9yvaD6gbKWx0WtA
    title: >
      [Last-Call] Artart last call review of draft-ietf-acme-subdomains-04
    author:
      name: Carsten Bormann

--- abstract

[^abs1-]

[^abs2-]

[^abs1-]: Normative documents that cite other normative documents often
    *restate* normative content extracted out of the cited document in
    their own words.

[^abs2-]: The present memo explains why this can be an Antipattern, and
    how it can be mitigated.

[^abs2i-]: The present memo explains why this can be an Antipattern
    {{KOENIG}}{{ANTIPATTERN}}, and how it can be mitigated.

--- middle

# Introduction

[^abs1-]

[^abs2i-]

## Conventions and Definitions

{::boilerplate bcp14info-tagged}

# The Restatement Anti-Pattern

A _Restatement_ is the attempted expression of information that is
already expressed elsewhere.

In this document, we are mostly concerned with _Normative
Restatements_, i.e., statements that are intended (or look like they
are intended!) to be normative.

Restatements are rarely verbatim copies of the original statement and
the context needed to interpret that, so they tend to introduce
uncertainty about the interpretation of the restatement.

Authors often presume a reader is well-versed enough to infer that
such an uncertainty (or outright contradiction) is not intended and
how it is to be resolved.
There is little reason to believe this is actually the case.

An _internal restatement_ is a restatement of information that has
been provided previously in the document under discussion.
Note that an unambiguous internal reference is not a restatement, as
it points to the original text and its context.
(There may still be uncertainties how to interpret the internal
restatement in the additional context.)

A reference is _unambiguous_ if the previous passage is clearly
identified and delimited.

An _external restatement_ is a restatement of information that has
been provided in (one or more) external documents.
Here there is increased danger of an unclear scope of the reference,
often by pointing to an entire document where only a specific passage
is actually intended to be referenced.

Restatements can be entirely _hidden_, i.e., there is no indication
that information given is a restatement.  Restatements can also be
_explicit_ by clearly being
identified as such, typically no longer using normative language.

Restatements can be an Anti-Pattern because they can be "a common
response to a recurring problem that is usually ineffective and risks
being highly counterproductive" {{WP-ANTIPATTERN}}.  {{reasons}} discusses
the recurring problems as perceived by document authors, {{perils}}
explains why restatements can be ineffective and counterproductive,
and {{defuse}} discusses how to use restatements in a way that is not.


# Reasons for making restatements {#reasons}

There are many reasons that cause document authors to include
restatements in their work, many of which are actually good reasons
once the perils of restatements are properly managed.

## Integrating a Complicated Base Standard Ecosystem

Sometimes the source of the actual normative statement is complex and
would require considerable time to digest.
A _simplifying_ restatement tries to shield the reader by rephrasing
or summarizing information from that source.

Such a restatement can be of good intention, or it can try to hide
complexity that the referencing document actually does make required to incur.

## Trying to be a Textbook for the Implementer

More generally, a restatement can attempt to be a directly useful
source for an implementer or user of a standard, e.g., by giving a
mere checklist of items (not necessarily complete!) that must be
implemented instead of actually identifying where the requirement and
possibly its finer points come from.

## Trying to Raise Attention to a Detail Deemed Surprising

The author of the referencing document may see a need to alert the
reader to a detail of the cited document that might seem unintuitive
(i.e., not familiar) to the author.  By restating the detail in terms
more familiar to readers of the referencing document, this alert can
be more useful.

## Bad formal description techniques

Formal description techniques (_FDT_, such as ABNF) are usually designed to
document a single specific artifact, not its evolution or its
embedding into another artifact.  This can lead to wholesale imports
of FDT material, without indication whether just the FDT was imported
or whether the importing document is intended to evolve with the donor
document.
See {{example-8288}} and {{example-6991}} for additional illustration of
this reason.

# Perils of restatements {#perils}

The danger of restatements is that they might not be exactly
expressing the same normative statement that the cited document makes.

One form of this is the _incomplete_ restatement.

Abridged copies of a normative statement from the cited document often
leave open whether the abridgment is intentional: Is the referencing
document only importing some of the requirements of the cited
document?
In the worst case, the restatement may appear to be _forking an
ecosystem_, i.e., an implementation of the cited document cannot be
used because it makes additional constraints that are not meant to be
included in the referencing document.
(This peril of course is also present with _intentional_ changes to
the normative statements in a cited document, but is likely to receive
much more attention during review.)

{{example-eat}} presents an example for the situation where a reader
might infer behavior based on the common law statute interpretation
rule:

> _"Expressio unius est exclusio alterius"_

which states that the reader is to presume that expressly referencing
one matter implies that other similar matters are intentionally not
mentioned and therefore are excluded.
This is particularly problematic with abridged statements, where this
rule may be invoked by the reader without an author being aware of it.

Restatements may be slightly _semantically different_ from the cited
document, in particular if the latter is based on a relatively
inaccessible (possibly poorly documented or poorly developed)
terminology.
Both authors and readers may not be aware that they need to use tools
that are commonplace in the ecosystem of the cited document.

A large danger originates from restatements that are unclear whether a
_new_ normative requirement is intended or a just a restatement of
known normative requirements of the cited document.  This is, of
course, particularly dangerous for _hidden_ restatements.

A restatement can cause _maintainability hazards_, as illustrated in
{{example-8288}}; it also can cause a referencing document to
_decouple_ from the ecosystem of a cited document once that is
repaired ({{example-6991}}).

Finally, to readers familiar with the cited document, the restatement
can be surprising; if there really is no information in the
restatement, the reader automatically searches for a specific reason
this restatement is made and starts to reinterpret it until it means
something specific that would justify its presence.
If the restatement is not clearly identified as such, this is likely
to cause misinterpretations, as if the usage envisioned attempts to
fork the cited ecosystem.
(Often, the people who need to interpret the document in question are
actually more familiar with the cited document and the surrounding
ecosystem than the authors of the referencing document, who may just
be pulling in the ecosystem to solve one of their problems.)

# Defusing restatements {#defuse}

A general recommendation for readers of a referencing document is that
they should try to detect restatements and read them in full knowledge
of their perils ({{perils}}).
If a resolution is required, the RFC errata process may provide a
(poor) mechanism to obtain the resolution and ensure it is documented
in the context of the referencing document.
Mailing list discussions are also a good way to obtain a resolution,
but for additional readers they can be hard to find, and, when found,
it can be hard to extract any consensus that was formed.

The rest of this section provides a summary of the recommendations
made by this document, employing {{RFC2119}} keywords as an instruction
to the potential implementers of this document, i.e., document authors
and reviewers.

Much of the danger of restatements can be averted if they are
sufficiently identified by the authors as such.

- For identification of internal restatements, use phrases such as:
  In other words, hence, in particular, as discussed in Section NN.
- For identification of external restatements: As described/defined in …
- In both cases, make sure that any local reference is clear and any
  non-local reference is resolvable and well-scoped.
- Rephrasing the statement as a Note can make clear that there is no
  normative intention.

If a larger copy from a cited document is made, it SHOULD be made
verbatim and differences introduced deliberately should be explicitly
identified, possibly in a second step.
Note that the FDT mechanisms and their evolution can make verbatim
copies less useful, in which case a systematic approach of first
copying and fixing and then, if necessary, modifying can help the
reader.
For instance, {{RFC2397}} uses a variant form of ABNF that can be
parsed only once the variant "`:=`" syntax is replaced by "`=`".
(This is an active specification and was cited as recently as in
{{Section 4.3 of RFC9399}}, which provides a clearly identified
restatement in modern ABNF, with errata applied and rules referenced
from elsewhere added \[we ignore the innocuous redefinition of "hex"
from "HEXDIG"].)

By making the copy informative, repairs from the base document (in the
{{RFC2397}} example e.g. {{errata2397}}) can be imported, even future
ones.

## Summary of Recommendations

(...Add nice checklist text for authors and reviewers based on {{defuse}} later...)

# Examples

## Example: Web linking {{RFC8288}} {#example-8288}

This example is about an internal, FDT-induced restatement in
{{RFC5988}}, which turned into an external restatement in {{RFC6690}},
which was not healed by the update to {{RFC5988}} in {{RFC8288}}.

{{Section 5 of RFC5988}} defines a serialization of web links in a Link Header Field.
A link can have zero of more `link-param` parameters, each of which
has the form (simplified):

~~~ abnf
link-extension = ( parmname [ "=" ( ptoken | quoted-string ) ] )
~~~

So link-extensions can always be written as a `quoted-string`, or,
alternatively, without quotes as a `ptoken` if the more limited character
repertoire of `ptoken`s suffices.

However, {{RFC5988}} also defines the specifics of a few link parameters.
When simply inserting this into the overall ABNF, the ABNF given for
these link parameters needs to _restate_ the ABNF
for link parameters in their common syntax (simplified):

~~~ abnf
link-param  = ( ( "rel" "=" relation-types )
              | ( "anchor" "=" <"> URI-Reference <"> )
              | ( "rev" "=" relation-types )
              | ( "hreflang" "=" Language-Tag )
              | ( "media" "=" ( MediaDesc | ( <"> MediaDesc <"> ) ) )
              | ( "title" "=" quoted-string )
              | ( "type" "=" ( media-type | quoted-mt ) )
~~~

This restatement loses the choice between `ptoken` and `quoted-string` for
many predefined link parameters, only keeping it for `"media"` and
`"type"` (and `"rel"` in the definition of `relation-types`, which is
arguably faulty by allowing non-ptoken characters in an unquoted URI).

One could say that this restatement was caused by a limitation of ABNF:
ABNF
cannot separately express both the overall syntax of link-params (which yields
the link-param value)) and the specific syntax for the predefined
link-params, contaminating the former with the latter.
The specific syntax would really need to be in terms of the value
yielded as opposed to *restating* the link-param syntax that yields the value.

{{Section 3 of RFC8288}} finally repairs this:

{:quote}
>     link-param = token BWS [ "=" BWS ( token / quoted-string ) ]
>
>   Note that any link-param can be generated with values using either
>   the token or the quoted-string syntax; therefore, recipients MUST be
>   able to parse both forms.  In other words, the following parameters
>   are equivalent:
>
>     x=y
>     x="y"
>
>   Previous definitions of the Link header did not equate the token and
>   quoted-string forms explicitly; the title parameter was always
>   quoted, and the hreflang parameter was always a token.  Senders
>   wishing to maximize interoperability will send them in those forms.
>
>   Individual link-params specify their syntax in terms of the value
>   after any necessary unquoting (as per {{RFC7230, Section 3.2.6}}).

Unfortunately, {{RFC6690}} adds an external restatement copying from
{{RFC5988}} in defining a few more link-params (simplified):

~~~ abnf
link-param     = ( ( "rel" "=" relation-types )  ; ...
                 / ( "type" "=" ( media-type / quoted-mt ) )
                 / ( "rt" "=" relation-types )
                 / ( "if" "=" relation-types )
                 / ( "sz" "=" cardinal )
cardinal       = "0" / ( %x31-39 *DIGIT )
~~~

The letter of this specification for instance prohibits `sz="47"`
(requiring this to be represented as `sz=47`).   The repair in
{{RFC8288}} cannot quite fix this as:

* it is not clear that the repair actually applies to {{RFC6690}} (a
  general problem with updated \["obsoleted"] references)
* the ABNF in {{RFC6690}} would need to be rewritten to apply the rule
  `cardinal` to the extracted value of the link-param.

## Example: Date-Time in YANG (RFC6991) {#example-6991}

{{RFC6991}} defines a YANG type `date-and-time` on page 11, restating
parts of {{RFC3339}} (the restatement is also faulty in its item (b), with an
attempted cleanup in {{I-D.ietf-netmod-rfc6991-bis}}).
Now that {{RFC3339}} is being bug-fixed via {{Section 2 of
I-D.ietf-sedate-datetime-extended}}, it is not clear whether the change
applies to the YANG type as well.
This is more of a problem for YANG than it might be otherwise, as it might trigger
the YANG concept of a "non-backwards-compatible" change to that
datatype — a problem that is not entirely *caused* by restatements but gets
much harder to discuss.

## Example: ACME for Subdomains (RFC9444-to-be) {#example-9444}

RFC9444-to-be defines a new feature added to {{RFC8555}}, referencing
the base standard in a number of places.

Reviewing the draft {{I-D.draft-ietf-acme-subdomains-04}}, {{acme-comment}} states:

> \## restatement vs. new normative content
>
> Providing a specification of a new feature added to ACME, the text
> explains a number basic ACME mechanisms that are relevant to this
> specification.
>
> One pervasive problem is that these restatements of RFC 8555 content
> are not always easy to distinguish from new, normative statements made
> by this document.
> E.g., 4.2 contains a statement about "is defined" that is part of a
> paragraph restating RFC 8555 -- this one, however, appears to be new
> normative content.
> (Languagetool diagnoses overuse of passive voice, which exacerbates
> this problem.)
>
> (The first paragraph of section 4 repeats the last paragraph of
> section 3.  But that is not a problem; redundancy can be good if it
> improves the flow, and this is clearly labeled as a restatement.)
> The introduction of section 4 is a summary/restatement of RFC 8555;
> section 4.1 introduces new normative content without warning (and
> leads the reader astray by actually referencing RFC 8555).

(These problems were addressed in a later draft of RFC9444-to-be.)


## Example: Base64 Encoding variants in draft-ietf-rats-eat-20 {#example-eat}

Base64 encoding is defined in {{RFC4648}}, but comes in a number of
variants.  These often have default settings that are to be used
"unless the specification referring to this document explicitly states
otherwise" (e.g., {{Section 3.2 of RFC4648}}).

Documents that reference {{RFC4648}} normatively are
surprisingly often sloppy in doing so.
Not {{I-D.draft-ietf-rats-eat-20}}: Its Section 2 (terminology) defines
the term "Base64url Encoding”, referencing {{RFC4648}} as well as
{{RFC7515}} to fill in the open questions from {{RFC4648}} (i.e., Section
5 and not Section 4, no '=' padding that would be default, no extra
characters).

While this was a good start, incomplete restatements in the following
text cause a problem {{rats-comment}}:

{:quote}
> A term "base64url encoded” \[...] is used in multiple places.  One of the
> places restates its own reference to RFC 4648, but doesn’t restate
> the reference to RFC 7515 and the text required with that.  This
> restatement is very misleading as it strongly implies RFC 7515 is
> *not* used here; the reference needs to be removed.  In the other
> places I find the term is simply used, which assumes the reader
> will think to look up the term in the terminology and make the
> match with the different term.  \[...]

(The problem in the draft was quickly addressed in the next revision.)

# Security Considerations

Restatements about security requirements and properties can create the
same uncertainties and interoperability problems as restatements in
other contexts.
Security considerations sections have turned out to be an attractor
for such problems.
They are meant "both to encourage document authors to consider
security in their designs and to inform the reader of relevant
security issues" {{Section 1 of -seccons}}.
In practice, they tend to be the first point in a document that
security issues are considered at all, so they often both contain
normative statements that are nowhere else in the document and
security-conscious restatements of other normative statements in the
document, the latter with all the perils that this memo is about.
The fact that security considerations sections are often heavily
fleshed out during IESG processing can exacerbate the problem.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

Julian Reschke opened the author's eyes to the fundamental problem of
restatements, possibly not using this word.
Many IETFers over decades have worked on mitigating restatements; the
author apologizes that examples in this memo naturally mainly come
from the author's own recollection.
