# Yellowgrid

### A mobile-first, responsive, proportional, BEM style, SCSS grid, with unlimited breakpoints and columns.

Features are:

- Unlimited number of columns
- Columns are proportional (%) to their parent
- Nestable grids
- Grid sets, with auto "row" clearing (IE9+)
- Reversible order
- Centering columns
- Pushing columns
- BEM syntax
- SCSS partials for importing
- Made for modern browsers, AKA *IE9+
- *And IE8, mostly:
    - Media query support requires a JS solution like [respond.js](https://github.com/scottjehl/Respond)
    - Grid set clearing uses nth-child, so a JS solution like [selectivizr](http://selectivizr.com/) would be required for that feature

Inspired heavily by:
  [Proportional Grids](https://github.com/mattberridge/Proportional-Grids/) (starting point)
  and [CSSWizardry Grids](https://github.com/csswizardry/csswizardry-grids) (theory and naming)

## Live demo

[Seeing > Reading](#)

## Basic configuration

Configuration is done in `_yellowgrid.scss`

```
// this is the fixed gutter between columns
$grid-gutter: 18px;

// number of columns you want
$grid-columns: 5;

// do you want grid sets?
$grid-sets : true;
// do you want set "rows" to autoclear? (IE9+)
$grid-sets-clearing : true;

// do you want push classes?
$grid-push : true;

// do you want centering classes?
$grid-center : true;

// these set your grid and column class names. Not recommended to change, but you can.
$grid-wrap-class: "grid";
$grid-col-class: "grid__col";
```

## Setting breakpoints

```
// Breakpoint vars
$bp-lap: 'only screen and (min-width: 500px)';
$bp-desk: 'only screen and (min-width: 979px)';

// Mobile first! no breakpoint
// Palm-based devices like a mobile phone
@include grids-init('palm');

// Breakpoint for lap-based devices like tablets, ipads, laptops
@media #{$bp-lap} {
    @include grid-setup('lap');
}

// Breakpoint for desk-based devices like computers or TVs
@media #{$bp-desk} {
    @include grid-setup('desk');
}
```

Set the breakpoint names and definitions as you please. `palm`, `lap`, and `desk` are arbitrary names that I like (from @CSSWizardry) to name the breakpoints.

## Default markup

```
<div class="grid">
    <div class="grid__col palm--1_2 lap--1_2 desk--1_3">
        amazing content
    </div>
</div>
```
- `.grid` wrap anything that you want to be a grid.
- `.grid__col` makes a column.
- `{namespace}--{size}` sets your widths and breakpoint controls.

## Example (compressed) file sizes:

  - fully loaded, 3 breakpoints, 5 columns = 7k
  - fully loaded, 3 breakpoints, 7 columns = 13.5k
  - bare minimum, 3 breakpoints, 5 columns = 1.7k

## Bonus breakpoint @mixin

Include or copy `_breakpoint.scss` to get access to a nifty breakpoint mixin that uses your `_yellowgrid.scss` breakpoint vars. Then go to town with

```
@include breakpoint('lap') {
    // lap+ styles
}
@include breakpoint('desk') {
    // desk+ styles
}
```
Include these "inline" to make responsive styling easy.
```
h1 {
    font-size: 2em;

    @include breakpoint('lap') {
        font-size: 2.5em;
    }

    @include breakpoint('desk') {
        font-size: 3em;
    }
}
```