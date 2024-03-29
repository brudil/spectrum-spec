# Spectrum Format Specification

Specification for the Spectrum content format.

**Version: 0.1**

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Overview](#overview)
- [Format](#format)
  - [Document/root](#documentroot)
  - [Subtypes](#subtypes)
    - [Article subtype](#article-subtype)
    - [Video subtype](#video-subtype)
  - [Sections 📝](#sections-%F0%9F%93%9D)
    - [Freeform 📝](#freeform-%F0%9F%93%9D)
    - [List 📝](#list-%F0%9F%93%9D)
  - [Streams 📝](#streams-%F0%9F%93%9D)
  - [Blocks](#blocks)
    - [Image block](#image-block)
    - [Video block](#video-block)
    - [Heading block](#heading-block)
    - [Text Block](#text-block)
    - [Quote block](#quote-block)
  - [Text Transformers](#text-transformers)
      - [Markdown](#markdown)
      - [Inlinedown](#inlinedown)
      - [Plaintext](#plaintext)
      - [HTML safe](#html-safe)
- [Implementation concepts](#implementation-concepts)
  - [Fields  📝](#fields--%F0%9F%93%9D)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


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

### Sections 📝

#### Freeform 📝

#### List 📝

### Streams 📝

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


### Text Transformers

Transformers have a common output: HTML.

- name: `'transformer'`
- transformer: name of transformer
- text: string


##### Markdown

- name: `'markdown'`

Transforms Markdown text.

##### Inlinedown

- name: `'inline'`

Transforms inline-level Markdown text. This essentially limits generated elements to anchors, emphasis and strong tags.

##### Plaintext

- name: `'plain'`

No transform.

##### HTML safe

- name: `'html'`

No transform. HTML directly injected. Does not escape.

## Implementation concepts

### Fields  📝