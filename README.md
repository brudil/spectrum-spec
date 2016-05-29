# Spectrum Format Specification

Specification for the Spectrum content format.

**Version: 0.1**

## Overview


## Format

### Document/root

The top level of Spectrum.

Fields:
- version: Number, version of spectrum spec document is using. Used for spectrum migrations
- content: Subtype, document content

```js
{
  "version": 0.1
  "content": SubtypeOutput
}
```

### Subtypes
Subtypes define the shape of the content. For example, an **Article** subtype might have a stream of blocks. Where as a **Video** subtype could also have a video block at its root level. A **gallery** subtype could deviate from the loose stream of blocks entirely to have a more structured stream of Image blocks.

Fields:
- _name: String, name of the subtype
- []: Properties, properties that define the subtype

#### Article subtype

Fields:
- name: `'article'`
- stream: `Stream` of sections

#### Video subtype

Fields:
- name: `'video'`
- featureVideo: `VideoBlock`
- stream: `Stream` of sections

### Properties

### Sections

### Streams

#### Wrapped Streams

### Blocks

Blocks are the containers of different types of media elements, for example videos, text, quotes, images and embeds.

#### Image block

Fields:
- name: `'image'`
- reference: `ImageResource`
- alt: `PlainTextTransformer`
- title: `PlainTextTransformer`
- caption: `InlinedownTextTransformer`
- source: `InlinedownTextTransformer`
- sourceURL: `String(validation=URL)`


#### Video block

Fields:
- name: `'video'`
- reference: `VideoResource`
- caption: `InlinedownTextTransformer`
- source: `InlinedownTextTransformer`
- sourceURL: `String(validation=URL)`


#### Heading block

Fields:
- name: `'heading'`
- level: Number(min=1, max=6)
- text: `InlinedownTextTransformer`


#### Text Block

Fields:
- name: `'text'`
- text: `MarkdownTextTransformer`


#### Quote block

- name: `'quote'`
- quote: `InlinedownTextTransformer`
- attributed: `InlinedownTextTransformer`


### Transformers

#### Text

##### Markdown

##### Inlinedown

##### Plain text

##### HTML safe
