# nva-language

## Status: Technical Note 
## Date: 2021-10-06

This document defines how languages are treated in the NVA technical platform.

## A note on the formulation of this document

Because language and identity are intertwined, an attempt has been made to use a system of representation that is inclusive and open for extension. The definitions below describe how languages are currently treated; this is subject to change. There are obvious lacks for those using sign language, minority languages and outside the European academic community.

In the document, language is defined as a system of communication regardless of medium of expression. One problem area is Norwegian, where Bokmål and Nynorsk are used in place of the spoken language — due to the overwhelming focus on written texts in the current development of NVA. Further development should include a distinction in cases of non-written language.

## How languages are represented

A language is represented in all-machine readable contexts as a Lexvo URI within the ISO 639-3 range. An example:

```
  http://lexvo.org/id/iso639-3/eng 
```
The reason that NVA uses the Lexvo URI is that it uniquely identifies a language with a known, external name (the HTTP-URI), and this allows NVA to align with other sources using the same URI.

Further, following the URI in the browser, you will note that Lexvo provides a wide range of data about a language, including mappings to other language identification systems and the name given to a language in multiple languages. The HTML view is a rendered version of a machine-readable data source, which allows NVA to work with other identification and naming systems.

### Machine readable data

Dereferencing the URI with appropriate headers (in this case `application/rdf+xml`) returns RDF for the element, other headers return the HTML page. Although RDF data is served (following a 303-redirect) via a http://lexvo.org/data/ URI, the http://lexvo.org/id/ URI MUST be used. Similarly, the HTML representation is served from a redirected `http://lexvo.org/page/` URI. This MUST not be used either.

To try out dereferencing, use the following CURL:

```
curl -L  -H "Accept: application/rdf+xml" http://lexvo.org/id/iso639-3/eng
```

Note that Lexvo *does not* support `https`.

## Using Lexvo-data in NVA

Although Lexvo provides a coherent system of information about many languages, it is impractical at the current time to use Lexvo directly due to technical and functional requirements. Thus, we use a subset of data, restricted to those languages that are in use in publishing in Norway — this set is defined simply in terms of the NVI (Norwegian Research Index) data for publications. This subset of languages may grow and NVA uses mechanisms to allow for this.

### Known languages

The subset of known languages is provided by the data in NVA itself, which is based on previously reported research activity. At the time of writing, this subset includes most European and a few non-European languages.

### Representing unknown languages

Using a known language means using a known URI. If a language is not known or is not defined, the URI `http://lexvo.org/id/iso639-3/und` is used, representing an undefined language. In the case that the language should be added to NVA, this information should be given to a local NVA administrator.

### Representing multiple languages

If several languages are used in a context (such as a written document) the URI `http://lexvo.org/id/iso639-3/mul` is used, which implies "Multiple languages". If the ISO 639-2/ISO 639-3 code `mis`(miscellaneous language) or related tokens is provided, it MUST be replaced by the expected represention (`mul`).

### Representing Norwegian language

Norwegian Bokmål and Nynorsk writing systems are to be annotated respectively with URIs `<http://lexvo.org/id/iso639-3/nob>` and `<http://lexvo.org/id/iso639-3/nno>`.

Norwegian `<http://lexvo.org/id/iso639-3/nor>` as a linguistic concept is not preferred and the of this is deferred to Bokmål `<http://lexvo.org/id/iso639-3/nob>`.

(This makes sense for most written texts, but is inappropriate for spoken language — currently, NVA focusses exclusively on written content.)

### Representing Sami languages

Sami languages are represented as Northern Sami `<http://lexvo.org/id/iso639-3/sme>`. This is done with an intention to represent the Sami languages with individual language codes from ISO 639-3, rather than a group code from ISO 639-5. Northern Sami was chosen initially because this is the largest language group in Norway and administrative sources group the languages together as "Samisk", creating a difficulty for non-Sami speakers to make a judgement.

### Uses of other systems

Some technical contexts require terms from BCP 47.

Conversions are used, from e.g. ISO 639-2, ISO 639-3 and language names, where a third-party source provides data in different formats.
