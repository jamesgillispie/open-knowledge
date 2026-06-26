---
type: note
title: Confluence Template — Generic Landing Page
description: Jane Street Confluence module specification template for the Generic Landing page (Pages content type).
tags:
  - client
  - jane-street
  - area17
---
# Confluence Template — Generic Landing Page

| | |
|---|---|
| **Content Type** | Pages |
| **Template** | Generic Landing |
| **Route** | /{parent-slug}/{child-slug} |
| **Content** | Blocks |
| **Ticket** | |

# Business Requirements

**Business Purpose**

- Page needs to serve whatever content strategy needs are assigned to it

**Current State**

- No CMS, pages need to be created ad hoc

**Strategic Recommendation**

- Create a flexible, elegant toolkit that meets the content needs of the system

# User Stories

**Page requirements - User**

- As a user, I want to accomplish my tasks quickly and easily, so that I can leave the website having achieved my goals.

**Page requirements - CMS admin**

- As an admin, I want to create, update and delete instances, so that I can manage the content.
- As an admin, I want to be able to assign the root of the generic landing page so that it can appear where it needs to in the URL structure.
- As an admin, I want to be able to nest generic landing pages so that I can create a parent-child relationship if needed.

# Functional Requirements

**Content model**

- Hero
- Slug
- Parent page
- Content (flexible blocks)
- SEO fields

**Nesting**

- A landing can have nested pages and those would simply be available in nested URL format /{parent-slug}/{child-slug}.
- Nesting example:
    - Page: “Membership”, slug membership, parent
    - Page: “Member resources”, slug resources, child
        - Field named “Parent page”: “Membership” is selected
    - URL: /membership/resources
- The reference “parent page” is used to determine the nested URL structure
- URL prefixes
    - visit
    - exhibitions-and-events
    - art
    - things-to-do
    - about
- URL prefix example:
    - Page: “Our mission”, slug: our-mission
    - Prefix: “about”
    - URL /about/our-mission
- URL prefix example with nesting:
    - Page: “Women artists”, slug: women-artists
    - Page: “Georgia O’Keefe”, slug: georgia-okeefe
        - Parent page: “Women artists”'
    - Prefix: “art”
    - URL /art/women-artists/georgia-okeefe

# Technical Specifications

**Module**

- Module name: Pages
- Singleton: No
- Translation:
- Published start/end date: No
- Ordering: No
- Nesting (parent and child relation): Yes

# CMS fields

| **Field Name** | **Field Type** | **Required** | **Limit** | **Field Options** | **Notes** |
|---|---|---|---|---|---|
| Title | Text | Yes | | | SEO default |
| Slug | Text, slug | Yes | | | |
| Parent | Ref: Pages | No | | | Single |
| Prefix | Ref: Pages: Prefixes | | Max 1 | visit, exhibitions-and-events, art, things-to-do, about | |
| Description | Textarea | | | | SEO default |
| Cover | Image | | | | SEO default |
| Content | Ref: Blocks | | | See list below | |
| SEO | Ref: SEO | | | | |

# Components Used

**Flexible**

- [Section title](https://area17.atlassian.net/wiki/spaces/JS/pages/682983425/Section+title)
- [Rich text editor](https://area17.atlassian.net/wiki/spaces/JS/pages/683114497/Rich+text+editor)
- [Link](https://area17.atlassian.net/wiki/spaces/JS/pages/682000387/Link)
- [Flexible multi-column text](https://area17.atlassian.net/wiki/spaces/JS/pages/681902091/Flexible+multi-column+text)
- [Gallery](https://area17.atlassian.net/wiki/spaces/JS/pages/683245583/Gallery)
- [Embed](https://area17.atlassian.net/wiki/spaces/JS/pages/683507714/Embed)
- [Quote](https://area17.atlassian.net/wiki/spaces/JS/pages/682393607/Quote)
- [Accordions](https://area17.atlassian.net/wiki/spaces/JS/pages/683638787/Accordions)
- [Storytelling block](https://area17.atlassian.net/wiki/spaces/JS/pages/682295311/Storytelling+block)
- [Flexible routing block](https://area17.atlassian.net/wiki/spaces/JS/pages/681541641/Flexible+routing+block)
- [Video routing](https://area17.atlassian.net/wiki/spaces/JS/pages/693534721/Video+routing)
- [Tabbed questions](https://area17.atlassian.net/wiki/spaces/JS/pages/693174276/Tabbed+questions)
- [Editorial listing](https://area17.atlassian.net/wiki/spaces/JS/pages/694943747/Editorial+listing)
- [Tabbed jobs listing](https://area17.atlassian.net/wiki/spaces/JS/pages/695795713/Tabbed+jobs+listing)

# Visual Design

## UX Wireframes

- Figma link

## UI Visual Design

_Include a link to Figma final designs and grab a small screenshot(s) for quick visual reference. Please include any significant style or breakpoint variants._

- Final Figma UI Visual Design

# Notes

## Links

## Questions

1. Can you confirm the list of URL prefixes that would be needed at launch?
2. What are the requirements for translation, if any?

# Changelog

| **Date** | **Source** | **Change description** |
|---|---|---|
| | | |
| | | |
