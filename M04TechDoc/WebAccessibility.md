# Web Accessibility
This document will attempt to convey a baseline knowledge of what web accessibility is and a few ways to implement it.

## Contents
1. What is it?
    - Main Categories to Consider
2. Ways to Support Each Type
3. Useful Tools

## What is it?
Web Accessibility is the practice of removing as much user friction as possible to those who are considered to have a disablility.
While there are many ways somebody can be disabled, the main categories web accessibility aims to ease difficulties for include:

### Main Categories to Consider:
1. Visual
    - blindness, low vision/poor eyesight, colorblindness
2. Motor/Mobility
    - difficulty or inability to use hands to manipulate a mouse
    - Parkinson's disease, muscular dystrophy, cerebral palsy, stroke, tremors, poor fine motor skills, etc.
3. Auditory
    - deafness/hard of hearing
4. Seizures
    - flashing lights, strobing effects, etc.
5. Cognitive and Intellectual 
    - developmental disabilities, learning difficulties (like dyslexia)
    - cognitive disabilities (PTSD, Alzheimers, Dementia etc)
    - anything that can affect memory, attention, problem solving, etc.

## Ways to Support Each Type

### Visual
To support individuals who are blind or have low vision, one of the best ways to support them is to use the proper tags for content being displayed on a webpage and 
to make heavy use of **aria tags**. Using the proper tag is as simple as using paragraphs `<p></p>` for blocks of text `<h1></h1>` headings for headers/categories/etc and to
avoid the overuse of `<div></div>` tags for every piece of content on a webpage. Aria (Accessible Rich internet Application) tags allows a developer to describe what a tag is and what it is used for. This can be helpful for individuals with screen readers, as the screen readers can use the aria tags to help with navigation. 
For individuals with colorblindness it is best to design your website with high contrast colors, especially for fonts. It is also recommended to avoid using colors that people are commonly colorblind to ie.Red/Green

### Motor/Mobility
For individuals with motor skill difficulties it is best to avoid requiring fine motor skills to use a website ie. clicking a small link. It is also best to make sure each component of a website is keyboard accessible, so that if a user does not have a mouse, they can still navigate through the website.

### Auditory
For individuals who are deaf/hard of hearing any content that is auditory should have an option for subtitles, transcription, and/or a video utilizing sign language available. Content should not require a user to be able to hear to access it (unless it is solely auditory like music for example, and even then it should still be accessible up to the point of playing the audio).

### Seizures
Avoid any flashing/strobing images, and if the content must contain flashing/strobing images, ensure that there is a warning and/or a user acknowledgment before showing such images. ie. TikTok when a video contains strobing/flashing lights showcases a warning before playing the video.

### Coginitive and Intellectual
The WCAG (Web Content Accessiblity Guidlines) put it better than I could:

- Guideline 1.3 Adaptable: Create content that can be presented in different ways (for example simpler layout) without losing information or structure.
- Guideline 1.4 Distinguishable: Make it easier for users to see and hear content including separating foreground from background.
- Guideline 2.2 Enough Time: Provide users enough time to read and use content.
- Guideline 2.4 Navigable: Provide ways to help users navigate, find content, and determine where they are.
- Guideline 3.1 Readable: Make text content readable and understandable.
- Guideline 3.2 Predictable: Make Web pages appear and operate in predictable ways.
- Guideline 3.3 Input Assistance: Help users avoid and correct mistakes.

## Useful Tools
- each browser has accessibility tools in their respective developer consoles. Use them to gauge how accessible your site is
- [WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/)
- [shadcn/ui](https://ui.shadcn.com/) a component library with some accessiblity built in.
- [bootstrap](https://getbootstrap.com/docs/4.4/getting-started/accessibility/) has some, but not all bases covered with accessibility
- [AccessibilityChecker.org](https://www.accessibilitychecker.org/) helps check if a website is compliant with accessibility standards
- [w3.org Tools List](https://www.w3.org/WAI/test-evaluate/tools/list/) contains a list of tools to check accessiblity



