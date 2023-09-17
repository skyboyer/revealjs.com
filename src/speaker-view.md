---
id: speaker-view
title: Speaker View
layout: default
---

# Speaker View

reveal.js comes with a speaker notes plugin which can be used to present "hidden" notes in a separate browser window. The notes window also gives you a preview of the next upcoming slide so it may be helpful even if you haven't written any notes. Press the »S« key on your keyboard to open the notes window.

A speaker timer starts as soon as the speaker view is opened. You can reset the timer by clicking on it.

## Speaker notes

Notes can be added to the slide or to the specific fragment. When added to fragment, notes will be shown only when that fragment is activated and will go away when you move to the next fragment.

There are two ways to add notes: either by adding `<aside class="notes">` element or by using `data-notes` attribute on `<section>` or fragment element.

```html
<section>
	<h2>Slide 1</h2>
	<div class="fragment">
		fragment 1
		<aside class="notes">Fragment-level note: 1</aside>
	</div>
	<div class="fragment" data-notes="fragment-level note: 2">
		fragment 2
	</div>
  <div class="fragment">
    fragment without notes
  </div>
	<aside class="notes">Slide-level notes</aside>
</section>
<section data-notes="Also slide-level notes">
	<h2>Slide 2</h2>
</section>
```

You can add the `data-markdown` attribute to the `<aside class="notes">` element if you prefer writing notes using Markdown:

```html
<section>
	<h2>Slide</h2>
	<aside class="notes" data-markdown>
		## subtitle
		**bold text**
	</aside>
</section>
```

When used locally, this feature requires that reveal.js [runs from a local web server](/installation/#full-setup).

```html/3-5
<section>
  <h2>Some Slide</h2>

  <aside class="notes">
    Shhh, these are your private notes 📝
  </aside>
</section>
```

If you're using the [Markdown](/markdown/) plugin, you can add notes with the help of a special delimiter:

```html/0-1,7-8
<section data-markdown="example.md" data-separator="^\n\n\n"
         data-separator-vertical="^\n\n" data-separator-notes="^Note:">
# Title
## Sub-title

Here is some content...

Note:
This will only display in the notes window.
</section>
```

## Adding the Speaker Notes Plugin

The plugin is already bundled with reveal.js. To enable the speaker notes plugin, add the plugin source to the `index.html` and add the plugin to the initialization of reveal.js.

```html
<script src="plugin/notes/notes.js"></script>
<script>
    Reveal.initialize({
        plugins: [ RevealNotes ]
    });
</script>
```

## Share and Print Speaker Notes

Notes are only visible to the speaker inside of the speaker view. If you wish to share your notes with others you can initialize reveal.js with the `showNotes` configuration value set to `true`. Notes will appear along the bottom of the presentations.

When `showNotes` is enabled notes are also included when you [export to PDF](/pdf-export/). By default, notes are printed in a box on top of the slide. If you'd rather print them on a separate page, after the slide, set `showNotes: "separate-page"`.

## Speaker Notes Clock and Timers

The speaker notes window will also show:

- Time elapsed since the beginning of the presentation.  If you hover the mouse above this section, a timer reset button will appear.
- Current wall-clock time
- (Optionally) a pacing timer which indicates whether the current pace of the presentation is on track for the right timing (shown in green), and if not, whether the presenter should speed up (shown in red) or has the luxury of slowing down (blue).

The pacing timer can be enabled by configuring the `defaultTiming` parameter in the `Reveal` configuration block, which specifies the number of seconds per slide.  120 can be a reasonable rule of thumb.  Alternatively, you can enable the timer by setting `totalTime`, which sets the total length of your presentation (also in seconds).  If both values are specified, `totalTime` wins and `defaultTiming` is ignored.  Regardless of the baseline timing method, timings can also be given per slide `<section>` by setting the `data-timing` attribute (again, in seconds).


## Server Side Speaker Notes

In some cases it can be desirable to run notes on a separate device from the one you're presenting on. The Node.js-based notes plugin lets you do this using the same note definitions as its client side counterpart. See <https://github.com/reveal/notes-server>.
