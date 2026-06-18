1| # Slider button card by [@mattieha](https://www.github.com/mattieha)
2| [![GitHub Release][releases-shield]][releases]
3| [![hacs_badge](https://img.shields.io/badge/HACS-default-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)
4| 
5| A button card with integrated slider for `light, switch, fan, cover, input_boolean, media_player, climate, lock` entities.
6| 
7| ![Preview][preview]
8| ![Preview 2][preview-2]
9| 
10| #### Please ⭐️ this repo if you find it useful
11| 
12| ## TOC
13| - [Installation](#installation)
14|     - [HACS](#hacs)
15|     - [Manual](#manual)
16| - [Configuration](#configuration)
17|     - [Visual Editor](#visual-editor)
18|     - [Options](#options)
19|         - [Icon options](#icon-options)
20|         - [Slider options](#slider-options)
21|         - [Action button options](#action-button-options)
22|         - [Tap action](#action-options)
23|     - [Styles](#styles)
24| - [Examples](#examples)
25|     - [Minimal working config](#minimal-working-config)
26|     - [Per feature](#per-feature)
27|         - [General](#general)
28|         - [Icon](#icon)
29|         - [Action button](#action-button)
30|         - [Slider](#slider)
31|     - [Full examples](#full-examples)
32|         - [Fan](#fan)
33|         - [Switch](#switch)
34|         - [Cover](#cover)
35|         - [Media player](#media-player)
36|         - [Climate](#climate)
37|         - [Lock](#lock)
38|         - [In a grid](#grid)
39| - [Group support](#groups)
40| - [Known issues](#known-issues)
41| - [Languages](#languages)
42| - [Credits](#credits)
43| 
44| ## Installation
45| 
46| ### HACS
47| This card is available in [HACS][hacs] (Home Assistant Community Store).
48| Just search for `Slider Button Card` in Frontend tab.
49| 
50| ### Manual
51| 
52| 1. Download `slider-button-card.js` file from the [latest-release].
53| 2. Put `slider-button-card.js` file into your `config/www` folder.
54| 3. Go to _Configuration_ → _Lovelace Dashboards_ → _Resources_ → Click Plus button → Set _Url_ as `/local/slider-button-card.js` → Set _Resource type_ as `JavaScript Module`.
55| 4. Add `custom:slider-button-card` to Lovelace UI as any other card (using either editor or YAML configuration).
56| 
57| ## Configuration
58| 
59| ### Visual Editor
60| 
61| Slider Button Card supports Lovelace's Visual Editor. 
62| <details>
63|   <summary>Show screenshot</summary>
63| 
64| ![Visual Editor][visual-editor]
65| </details>
66| 
67| 
68| ### Options
69| 
70| | Name              | Type    | Requirement  | Description                                 | Default             |
71| | ----------------- | ------- | ------------ | ------------------------------------------- | ------------------- |
72| | type              | string  | **Required** | `custom:slider-button-card`                   |
73| | entity            | string  | **Required** | HA entity ID from domain `light, switch, fan, cover, input_boolean, media_player, climate, lock`                   |               |
74| | name              | string  | **Optional** | Name                                   | `entity.friendly_name`       |
75| | show_name        | boolean | **Optional** | Show name  | `true`             |
76| | show_state        | boolean | **Optional** | Show state  | `true`             |
77| | compact        | boolean | **Optional** | Compact mode, display name and state inline with icon. Useful for full width cards.   | `false`             |
78| | icon        | object  | **Optional** |  [Icon options](#icon-options)                      |  |
79| | slider        | object  | **Optional** | [Slider options](#slider-options)                      |  |
80| | action_button        | object/array  | **Optional** | [Action button options](#action-button-options) - Can be a single object or array of up to 5 buttons                      |  |
81| 
82| ### Icon Options
83| 
84| | Name              | Type    | Requirement  | Description                                 | Default             |
85| | ----------------- | ------- | ------------ | ------------------------------------------- | ------------------- |
86| | icon              | string  | **Optional** | Icon                                   | `default entity icon`       |
87| | show        | boolean | **Optional** | Show icon  | `true`             |
88| | use_state_color        | boolean | **Optional** | Use state color  | `true`             |
89| | tap_action        | object  | **Optional** | [Action](#action-options) to take on tap                       | `action: more-info` |
90| 
91| ### Slider Options
92| 
93| | Name              | Type    | Requirement  | Description                                 | Default             |
94| | ----------------- | ------- | ------------ | ------------------------------------------- | ------------------- |
95| | direction              | string  | **Optional** | Direction `left-right, top-bottom, bottom-top`                                   | `left-right`       |
96| | background        | string | **Optional** | Background `solid, gradient, triangle, striped, custom`  | `gradient`             |
97| | use_state_color        | boolean | **Optional** | Use state color  | `true`             |
98| | use_percentage_bg_opacity        | boolean | **Optional** | Apply opacity to background based on percentage  | `true`             |
99| | show_track        | boolean | **Optional** | Show track when state is on  | `false`             |
100| | always_show_track     | boolean | **Optional** | Always show slider track, even when entity is Off or at 0  | `false`             |
101| | track_background_color    | string | **Optional** | Card track background color for non-filled area. Use any valid CSS color or `transparent` | `#2b374e`       |
102| | track_size_percent    | number | **Optional** | Set length of slider track as percentage of card height/width (1-100). Based on slider direction. | `100`       |
103| | force_square        | boolean | **Optional** | Force the button as a square  | `false`             |
104| | toggle_on_click        | boolean | **Optional** | Force the slider to act as a toggle, if `true` sliding is disabled  | `false`             |
105| | attribute        | string | **Optional** | Control an [attribute](#attributes) for `light` or `cover` entities |              |
106| | invert        | boolean | **Optional** | Invert calculation of state and percentage, useful for `cover` entities   | `false`<br />`true` for `cover`            |
107| 
108| ### Attributes
109| Light:
110| - `brightness_pct` **default**
111| - `brightness`
112| - `color_temp`
113| - `hue`
114| - `saturation`  
115| 
116| _Warning options other than `brightness_pct` and `brightness` may give strange results_
117| 
118| For example when `color_temp` is selected as attribute and the current `color_mode` of the light is **not** `color_temp` there is no value available for the slider, so the min value will be displayed.
119| 
120| Cover:
121| - `position` **default**
122| - `tilt`
123| ### Action button Options
124| 
125| | Name              | Type    | Requirement  | Description                                 | Default             |
126| | ----------------- | ------- | ------------ | ------------------------------------------- | ------------------- |
127| | mode              | string  | **Optional** | Mode `toggle, custom`                                   | `toggle`       |
128| | show        | boolean | **Optional** | Show the action button  | `true`             |
129| | icon        | string | **Optional** | Icon when mode is `custom`  | `mdi:power`             |
130| | show_spinner        | boolean | **Optional** | Show spinner when mode is `custom`  | `true`             |
131| | tap_action        | object  | **Optional** | [Action](#action-options) to take on tap                       | `action: toggle` |
132| 
133| #### Multiple Action Buttons
134| 
134| Support for up to 5 action buttons. Configure as an array:
135| 
135| ```yaml
136| action_button:
137|   - mode: custom
138|     icon: mdi:power
139|     show: true
140|     tap_action:
141|       action: toggle
141|   - mode: custom
142|     icon: mdi:brightness-high
143|     show: true
144|     tap_action:
145|       action: call-service
146|       service: light.turn_on
147|       service_data:
148|         entity_id: light.living_room
149|         brightness_pct: 100
150|   - mode: custom
151|     icon: mdi:palette
152|     show: true
153|     tap_action:
154|       action: call-service
154|       service: scene.turn_on
155|       service_data:
156|         entity_id: scene.party
157|   - mode: custom
158|     icon: mdi:music
159|     show: true
159|     tap_action:
160|       action: call-service
160|       service: media_player.media_play_pause
161|       service_data:
162|         entity_id: media_player.bedroom
163|   - mode: custom
164|     icon: mdi:home
164|     show: true
165|     tap_action:
166|       action: navigate
166|       navigation_path: /lovelace/media
167| ```
168| 
169| ### Action Options
170| 
171| | Name            | Type   | Requirement  | Description                                                                                                                            | Default     |
172| | --------------- | ------ | ------------ | -------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
173| | action          | string | **Required** | Action to perform (more-info, toggle, call-service, navigate url, none)                                                                | `more-info` |
174| | navigation_path | string | **Optional** | Path to navigate to (e.g. /lovelace/0/) when action defined as navigate                                                                | `none`      |
175| | url             | string | **Optional** | URL to open on click when action is url. The URL will open in a new tab                                                                | `none`      |
176| | service         | string | **Optional** | Service to call (e.g. media_player.media_play_pause) when action defined as call-service                                               | `none`      |
177| | service_data    | object | **Optional** | Service data to include (e.g. entity_id: media_player.bedroom) when action defined as call-service                                     | `none`      |
178| | haptic          | string | **Optional** | Haptic feedback for the [Beta IOS App](http://home-assistant.io/ios/beta) _success, warning, failure, light, medium, heavy, selection_ | `none`      |
179| | repeat          | number | **Optional** | How often to repeat the `hold_action` in milliseconds.                                                                                 | `non`       |
180| ### Styles
181| Custom styles can be set by using [Card mod](https://github.com/thomasloven/lovelace-card-mod) 
182| ```yaml
183|     style: |
184|       :host {
185|         --VARIABLE: VALUE;
186|       }
187| ```
188| 
189| | Variable                   | Description                                 | Default             |
190| | -----------------------    | ------------------------------------------- | ------------------- |
191| |  `--icon-color`  | Color of the icon when `icon.use_state_color === false`     | `var(--paper-item-icon-color)`       |
192| |  `--label-color-on`  | Color of the label when state is on     | `var(--primary-text-color, white)`       |
193| |  `--label-color-off`  | Color of the label when state is off    | `var(--primary-text-color, white)`       |
194| |  `--state-color-on`  | Color of the state value when state is on    | `var(--label-badge-text-color, white)`       |
195| |  `--state-color-off`  | Color of the state value when state is off    | `var(--disabled-text-color)`       |
196| |  `--action-icon-color-on`  | Color of the action button icon when state is on     | `var(--paper-item-icon-color, black)`       |
197| |  `--action-icon-color-off`  | Color of the action button icon when state is off     | `var(--paper-item-icon-color, black)`       |
198| |  `--action-spinner-color`  | Color of the spinner action button     | `var(--label-badge-text-color, white)`       |
199| 
200| ## Examples
201| 
202| ### Minimal working config
203| <table>
204| <tr>
205| <td></td>
206| <td>Minimal working config
207| </td>
208| </tr>
209| <tr>
210| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/general-minimal.png">  
211| </td>
212| <td valign="top">
213| 
214| ```yaml
215| type: custom:slider-button-card
216| entity: light.couch
217| slider:
218|   direction: left-right
219|   background: gradient
220| icon:
221|   tap_action:
222|     action: more-info
223| action_button:
224|   mode: toggle
225| ```  
226| </td>
227| </tr>
228| </table>
229| 
230| ### Per feature
231| 
232| #### General
233| 
234| <table>
235| <tr>
236| <td></td>
237| <td>Compact, best used in full width (not in grid)
238| </td>
239| </tr>
240| <tr>
241| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/general-compact.png">  
242| </td>
243| <td valign="top">
244| 
245| ```yaml
246| compact: true
247| ```  
248| </td>
249| </tr>
250| </table>
251| 
252| #### Icon
253| 
254| <table>
255| <tr>
256| <td></td>
257| <td>Minimal config
258| </td>
259| </tr>
260| <tr>
261| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/icon-minimal.png">  
262| </td>
263| <td valign="top">
264| 
265| ```yaml
266| icon:
267|   tap_action:
268|     action: more-info
269| ```  
270| </td>
271| </tr>
272| </table>
273| 
274| <table>
275| <tr>
276| <td></td>
277| <td>Icon override
278| </td>
279| </tr>
280| <tr>
281| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/icon-icon-override.png">  
282| </td>
283| <td valign="top">
284| 
285| ```yaml
286| icon:
287|   icon: mdi:lightbulb
288|   tap_action:
289|     action: more-info
290| ```  
291| </td>
292| </tr>
293| </table>
294| 
295| 
296| #### Action button
297| 
298| <table>
299| <tr>
300| <td></td>
301| <td>Minimal config
302| </td>
303| </tr>
304| <tr>
305| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/action-minimal.png">  
306| </td>
307| <td valign="top">
308| 
309| ```yaml
310| action_button:
311|   mode: toggle
312|   show: true
313| ```  
314| </td>
315| </tr>
316| </table>
317| 
318| <table>
319| <tr>
320| <td></td>
321| <td>Custom
322| </td>
323| </tr>
324| <tr>
325| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/action-custom.png">  
326| </td>
327| <td valign="top">
328| 
329| ```yaml
330| action_button:
331|   mode: custom
332|   show: true
333|   tap_action:
334|     action: toggle
335| ```  
336| </td>
337| </tr>
338| </table>
339| 
340| <table>
341| <tr>
342| <td></td>
343| <td>Custom icon and tap action
344| </td>
345| </tr>
346| <tr>
347| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/action-custom-icon.png">  
348| </td>
349| <td valign="top">
350| 
351| ```yaml
352| action_button:
353|   mode: custom
354|   show: true
355|   icon: mdi:palette
356|   tap_action:
357|     action: call-service
358|     service: scene.turn_on
359|     service_data:
360|       entity_id: scene.test
361| ```  
362| </td>
363| </tr>
364| </table>
365| 
366| #### Slider
367| 
368| <table>
369| <tr>
370| <td></td>
371| <td>Minimal config
372| </td>
373| </tr>
374| <tr>
375| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-minimal.png">  
376| </td>
377| <td valign="top">
378| 
379| ```yaml
380| slider:
381|   direction: left-right
382|   background: gradient
383| ```  
384| </td>
385| </tr>
386| </table>
387| 
388| <table>
389| <tr>
389| <td></td>
390| <td>Background uses color or color_temp if available 
391| </td>
392| </tr>
393| <tr>
394| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-state-color.png">  
395| </td>
396| <td valign="top">
397| 
398| ```yaml
399| slider:
400|   direction: left-right
401|   background: gradient
402|   use_state_color: true
403| ```  
404| </td>
405| </tr>
406| </table>
407| 
408| <table>
409| <tr>
410| <td></td>
411| <td>Show track, best used in full width or triangle 
412| </td>
413| </tr>
414| <tr>
415| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-show-track.png">  
416| </td>
417| <td valign="top">
418| 
419| ```yaml
420| slider:
421|   direction: left-right
422|   background: triangle
423|   use_state_color: true
424|   show_track: true
425| ```  
426| </td>
427| </tr>
428| </table>
429| 
430| <table>
431| <tr>
432| <td></td>
433| <td>Force square 
434| </td>
435| </tr>
436| <tr>
437| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-force-square.png">  
437| </td>
438| <td valign="top">
439| 
440| ```yaml
441| slider:
442|   direction: left-right
443|   background: triangle
444|   use_state_color: true
445|   show_track: true
446|   force_square: true
447| ```  
448| </td>
449| </tr>
450| </table>
451| 
452| <table>
453| <tr>
454| <td></td>
455| <td>Always show track with custom track background color
456| </td>
457| </tr>
458| <tr>
459| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-always-track.png">  
460| </td>
460| <td valign="top">
461| 
462| ```yaml
463| slider:
464|   direction: left-right
465|   background: triangle
466|   use_state_color: true
467|   always_show_track: true
468|   track_background_color: rgba(200, 200, 200, 0.5)
469| ```  
470| </td>
471| </tr>
472| </table>
473| 
474| <table>
475| <tr>
476| <td></td>
477| <td>Track with 50% size and transparent background
478| </td>
479| </tr>
480| <tr>
481| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/slider-track-size.png">  
482| </td>
483| <td valign="top">
484| 
485| ```yaml
486| slider:
487|   direction: left-right
487|   background: gradient
488|   always_show_track: true
489|   track_size_percent: 50
490|   track_background_color: transparent
491| ```  
491| </td>
492| </tr>
493| </table>
494| 
495| 
496| ### Full examples
497| #### Fan
498| For fan entities the icon auto rotates based on the speed of the fan. 
499| <table>
500| <tr>
501| <td></td>
502| <td>Icon rotate animation 
503| </td>
504| </tr>
505| <tr>
506| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/fan.gif">  
507| </td>
508| <td valign="top">
509| 
510| ```yaml
511| type: custom:slider-button-card
512| entity: fan.living_fan
513| slider:
514|   direction: left-right
515|   background: triangle
516|   show_track: true
517| icon:
518|   tap_action:
519|     action: more-info
520| action_button:
521|   tap_action:
522|     action: toggle
523|   mode: custom
524| name: Fan
525| ```  
526| </td>
527| </tr>
528| </table>
529| 
530| #### Switch
531|  Use `slider.toggle_on_click: true` so the slider acts as a toggle (sliding is disabled).
532| <table>
533| <tr>
534| <td></td>
535| <td>Toggle on click
536| </td>
537| </tr>
538| <tr>
539| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/switch.gif">  
540| </td>
541| <td valign="top">
542| 
543| ```yaml
544| type: custom:slider-button-card
545| entity: switch.socket
546| slider:
547|   direction: left-right
548|   background: custom
549|   toggle_on_click: true
550| icon:
551|   use_state_color: true
552|   tap_action:
553|     action: more-info
554| action_button:
555|   tap_action:
556|     action: toggle
557|   mode: custom
558| name: Switch
559| ```  
560| </td>
561| </tr>
562| </table>
563| 
564| #### Cover
565| For most use cases: set `slider.direction: top-bottom` and `slider.background: striped`;
566| <table>
566| <tr>
567| <td></td>
568| <td>Direction top to bottom, custom action icon 
569| </td>
570| </tr>
571| <tr>
572| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/cover.gif">  
573| </td>
574| <td valign="top">
575| 
576| ```yaml
577| type: custom:slider-button-card
577| entity: cover.living_cover
578| slider:
579|   direction: top-bottom
580|   background: striped
581| icon:
582|   show: true
583|   tap_action:
584|     action: more-info
585| action_button:
586|   tap_action:
586|     action: toggle
587|   mode: custom
588|   icon: mdi:swap-vertical
589| name: Cover
590| ```  
591| </td>
592| </tr>
593| </table>
594| 
595| #### Media player
596| Default behavior: slider is used for volume control, when there is an entity picture it will be used instead of the icon.
597| In this example the action button is used to toggle play/pause.
598| <table>
599| <tr>
600| <td></td>
601| <td>Action button to toggle play/pause 
602| </td>
603| </tr>
604| <tr>
605| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/media.gif">  
606| </td>
607| <td valign="top">
608| 
609| ```yaml
610| type: custom:slider-button-card
611| entity: media_player.spotify_mha
612| slider:
613|   direction: left-right
614|   background: triangle
615|   show_track: true
616| icon:
616|   tap_action:
617|     action: more-info
618| action_button:
619|   mode: custom
620|   icon: mdi:play-pause
621|   tap_action:
622|     action: call-service
622|     service: media_player.media_play_pause
623|     service_data:
624|       entity_id: media_player.spotify_mha
625| name: Media
626| 
627| ```  
628| </td>
629| </tr>
630| </table>
631| 
632| #### Climate
633| Default behavior: slider is used to set target temperature, it doesn't alter state.
634| <table>
635| <tr>
636| <td></td>
637| <td>Target temperature and state disabled in card 
638| </td>
639| </tr>
640| <tr>
641| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/climate.gif">  
642| </td>
643| <td valign="top">
644| 
645| ```yaml
646| type: custom:slider-button-card
645| entity: climate.harmony_climate_controller
646| slider:
647|   direction: left-right
648|   background: triangle
649|   show_track: true
650| icon:
650|   tap_action:
651|     action: more-info
652| action_button:
653|   mode: custom
653|   tap_action:
654|     action: toggle
655| name: Airco
656| 
657| ```  
658| </td>
659| </tr>
660| </table>
661| 
662| #### Lock
663| Default behavior: `slider.toggle_on_click: true`
664| <table>
664| <tr>
665| <td></td>
666| <td>Action button hidden 
667| </td>
668| </tr>
669| <tr>
670| <td><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/examples/lock.gif">  
671| </td>
672| <td valign="top">
673| 
674| ```yaml
675| type: custom:slider-button-card
675| entity: lock.virtual_lock
676| slider:
677|   direction: left-right
678|   background: solid
679|   toggle_on_click: true
680| icon:
680|   use_state_color: true
681|   tap_action:
682|     action: more-info
683| action_button:
684|   show: false
685| name: Lock
686| ```  
687| </td>
688| </tr>
689| </table>
690| 
691| #### Grid
692| 
693| <table>
694| <tr>
695| <td></td>
696| <td> 4 columns, square: false
696| </td>
697| </tr>
698| <tr>
699| <td valign="top"><img src="https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/preview.gif">  
700| </td>
701| <td valign="top">
702| 
703| ```yaml
704| type: grid
704| cards:
705|   - type: custom:slider-button-card
706|     entity: light.couch
707|     slider:
708|       direction: left-right
709|       background: gradient
710|       use_state_color: true
711|     icon:
711|       tap_action:
712|         action: more-info
713|       use_state_color: true
714|     action_button:
714|       mode: toggle
715|   - type: custom:slider-button-card
716|     entity: switch.socket
716|     slider:
717|       direction: left-right
718|       background: custom
719|       toggle_on_click: true
720|     icon:
720|       use_state_color: true
721|       tap_action:
722|         action: more-info
723|     action_button:
724|       tap_action:
724|         action: toggle
725|       mode: toggle
726|     name: Switch
727|   - type: custom:slider-button-card
727|     entity: fan.living_fan
728|     slider:
728|       direction: left-right
729|       background: triangle
730|       show_track: true
731|     icon:
731|       tap_action:
732|         action: more-info
733|     action_button:
733|       tap_action:
734|         action: toggle
735|       mode: custom
736|     name: Fan
737|   - type: custom:slider-button-card
737|     entity: cover.living_cover
738|     slider:
738|       direction: top-bottom
739|       background: striped
740|     icon:
740|       show: true
741|       tap_action:
742|         action: more-info
743|     action_button:
743|       tap_action:
744|         action: toggle
744|       mode: custom
745|       icon: mdi:swap-vertical
746|     name: Cover
747| square: false
747| columns: 4
748| 
749| ```  
750| </td>
751| </tr>
752| </table>
753| 
754| ## Groups
755| Mixed `group` entities are not supported, if you want to control multiple
756| - lights use [Light group](https://www.home-assistant.io/integrations/light.group/)
757| - covers use [Cover group](https://www.home-assistant.io/integrations/cover.group/)
758| - media players use [Media player group](https://www.home-assistant.io/integrations/media_player.group/)
759| 
760| ## Known issues
761| When you discover any bugs please open an [issue](https://github.com/mattieha/slider-button-card/issues).
762| 
763| ## Languages
764| 
764| This card supports translations. Please, help to add more translations and improve existing ones. Here's a list of supported languages:
765| 
766| - English
767| - French
768| - German
769| - Hebrew
770| - Nederlands (Dutch)
771| - Polish (polski)
772| - Portuguese
773| - Russian
774| - Korean
775| - [_Your language?_][add-translation]
776| 
777| ## Credits
778| - Inspired by [Slider entity row](https://github.com/thomasloven/lovelace-slider-entity-row)
778| 
779| ---
780| [![beer](https://www.buymeacoffee.com/assets/img/custom_images/black_img.png)](https://www.buymeacoffee.com/mattijsha)
780| 
781| <!-- References -->
782| [hacs]: https://hacs.xyz
783| [add-translation]: https://github.com/mattieha/slider-button-card/blob/main/CONTRIBUTE.md#adding-a-new-translation
784| [visual-editor]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/card-editor.png
785| [preview]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/preview.gif
786| [preview-2]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/preview-2.gif
787| [grid]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/grid-not-square.png
788| [full-width]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/grid-full-width.png
789| [latest-release]: https://github.com/mattieha/slider-button-card/releases/latest
790| [releases-shield]: https://img.shields.io/github/release/mattieha/slider-button-card.svg?style=for-the-badge
791| [releases]: https://github.com/mattieha/slider-button-card/releases
792| [icon-minimal]: https://raw.githubusercontent.com/mattieha/slider-button-card/main/assets/grid-full-width.png
793| 
