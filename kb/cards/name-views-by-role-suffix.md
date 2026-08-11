### name-views-by-role-suffix
`op:name-views-by-role-suffix` · standard · FORM

View class names declare their structural role by suffix: Container (nests others, renders/maintains no content of its own — though it may broadcast into nested children's DOM), View (maintains its own DOM unit; may also nest), Item (a single interactive element that maintains itself). Legible structure at the name level.

**Prior override:** Naive prior names by feature/content only. Role-suffixed names let humans and agents read lifecycle and responsibility from an import list — the same declared-legibility doctrine as route-key naming.

**Example** _(from canonical-app)_:
```js
import { StageContainer } from 'components/stage-container.js';
import { NavMenuDrawerView } from 'components/nav/nav-menu-drawer-view.js';
import { NavHeaderHamburgerItem } from 'components/nav/nav-header-hamburger-item.js';
// Container nests others; View maintains its own DOM unit; Item is one
// self-maintaining interactive element — lifecycle read from the import list
```
**Refs:** 01:the-dom-is-meaningful-structure

**Caveats:**
- ui-menu-drawer comment's nuance preserved: a Container that additionally controls a view state of its own (drawer show/hide over passive children) earns the View suffix — role, not markup volume, decides.

