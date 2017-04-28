[![GitHub issues](https://img.shields.io/github/issues/bmatto/cellulose.svg)](https://github.com/bmatto/cellulose/issues)
[![CircleCI](https://img.shields.io/circleci/project/github/bmatto/cellulose.svg)]()
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/bmatto/cellulose/master/LICENSE)

# Cellulose

Cellulose is a React layout library that allows you to create contextually aware components using flexbox.

The `<Cellulose>` component uses its own rendered width to assign style and responsive behavior, rather than the width of the browser window.

## Installation

`npm i -S cellulose` or `yarn add cellulose`

## Usage

Use the `<Cellulose>` component to define a container that you want to style based on internal width.

`<Cellulose>` will render into the DOM as a `<div>` whose class is determined by which breakPoint in `breakPoints` its own width exceeds.

```
import { Cellulose } from 'cellulose'
import React from 'react'

export function MyComponent() {
  const breakPoints = {
    768:  'greater-than-768',
    1024: 'greater-than-1024'
  }

  return (
    <Cellulose breakPoints={breakPoints}>
      <div>Content</div>
    </Cellulose>
  )
}
```

Cellulose can also be used to create a responsive grid. Use the prop `columns=` of `<Cellulose>` to define the number of columns to use, then add `<Cell>` components with `spanOptions` props that define responsive behavior

```
import { Cellulose, Cell } from 'cellulose'
import React from 'react'

export function MyComponent() {
  const breakPoints = {
    768:  'greater-than-768',
    1024: 'greater-than-1024'
  }

  return (
    <Cellulose columns={12} breakPoints={breakPoints}>
      <Cell spanOptions={{ 768: 6, 1024: 8 }}>
        <div>One</div>
      </Cell>
      <Cell spanOptions={{ 768: 6, 1024: 4 }}>
        <div>Two</div>
      </Cell>
    </Cellulose>
  )
}
```

Cellulose's `<Cell>` components can even configure their own classes based on which `breakPoints` are activated!

```
import { Cellulose, Cell } from 'cellulose'
import React from 'react'

export function MyComponent() {
  const breakPoints = {
    768:  'greater-than-768',
    1024: 'greater-than-1024'
  }

  return (
    <Cellulose columns={12} breakPoints={breakPoints}>
      <Cell
          spanOptions={{
            768: { cols: 1, className: 'tabletMenu' },
            1024: { cols: 2, className: 'desktopMenu' }
          }}>
        <div>Menu-ish Stuff</div>
      </Cell>
      <Cell
          spanOptions={{
            768: { cols: 11, className: 'tabletContent' },
            1024: { cols: 10, className: 'desktopContent' }
          }}>
        <div>Body Content</div>
      </Cell>
    </Cellulose>
  )
}
```

## Cellulose Props

Prop | Type | Usage
-----|------|------
columns | Number | # of columns for Cellulose's internal grid
breakPoints | Object Number:String | Key: The minimum pixels for this breakpoint. Value: The class to assign to the component while this breakpoint is active

## Cell props

Prop | Type | Usage
-----|------|------
spanOptions | Object Number:Number or Number:Object | Key: should be a key from Cellulose breakPoints prop keys. Value: If Number, the number of columns this Cell should consume at this breakpoint. If object, see `spanOptions props` heading below for possible props

## spanOptions props
Prop | Type | Usage
-----|------|------
cols | Number | the number of columns this Cell should consume at this breakpoint
className | String | class to apply to Cell when this breakpoint is active
