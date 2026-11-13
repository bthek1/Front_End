# Front End

What the user actually sees: the web platform itself, the JavaScript ecosystem on top of it, and the Python shortcuts for when you do not want any of that.

Author

Benedict Thekkel

There are two routes to a user interface here, and the site covers both without pretending one is correct.

The first is the real one: HTML, CSS, JavaScript, then a framework, a bundler, a linter, and a build step. The second is to skip it, and let a Python library generate the interface. That is the right answer more often than front-end developers like to admit, particularly for a dashboard or a model demo, which is most of what gets built in this collection.

Before either route there is a third thing, which is deciding what the interface should be at all. The design pages below cover that, and they are the only part of this site that is not about a tool.

Nearly every page assumes a Django REST Framework backend, because that is what these interfaces are put in front of. See [Back End](https://bthek1.github.io/Back_End/) for that half.

------------------------------------------------------------------------

## Design: UI and UX

Twelve pages on designing the interface rather than building it, ordered the way the work runs: understand people, structure the content, design the behaviour, then the surface, then evaluate it. Every page ends with a section on how that discipline fails in practice, which is usually the fastest part to read.

**Understanding users and content**

| Page | Covers |
|----|----|
| [UX Research](UI_UX/ux_research.llms.md) | Interviews, contextual inquiry, surveys, diary studies, affinity mapping, personas and jobs-to-be-done, journey maps, and how many participants is enough |
| [Information Architecture](UI_UX/information_architecture.llms.md) | Content inventory, organisation schemes, the four navigation models, labelling, card sorting, tree testing, search, and URLs as interface |

**Designing behaviour and surface**

| Page | Covers |
|----|----|
| [Interaction Design](UI_UX/interaction_design.llms.md) | Flows, the eight screen states nobody designs, affordances and signifiers, feedback timing, forms, progressive disclosure, undo over confirmation, and Nielsen’s ten heuristics |
| [Visual Design Foundations](UI_UX/visual_design_foundations.llms.md) | Hierarchy, grids, the spacing scale, type scale and measure, colour as roles rather than a palette, Gestalt grouping, elevation, and icons |
| [Design Systems and Tokens](UI_UX/design_systems_and_tokens.llms.md) | The three token tiers, naming by role, one source of truth to many platforms, theming light and dark, component API design, versioning, and when not to build a system |
| [Responsive and Multiplatform](UI_UX/responsive_and_multiplatform.llms.md) | Content-driven breakpoints, fluid type with `clamp()`, container queries, touch versus pointer versus keyboard, platform conventions, density, internationalisation and right-to-left |
| [Content Design and Motion](UI_UX/content_design_and_motion.llms.md) | Voice and tone, microcopy, error messages that say what to do, empty states, readability, then animation duration and easing, and perceived performance |

**Constraints and validation**

| Page | Covers |
|----|----|
| [Accessibility](UI_UX/accessibility.llms.md) | WCAG 2.2 AA, POUR, semantic HTML over ARIA, keyboard and focus management, accessible names and live regions, contrast, the 2.2 additions, alt text, and how to test |
| [Prototyping and Handoff](UI_UX/prototyping_and_handoff.llms.md) | Choosing fidelity, wireframing with real content, Figma auto layout, variants and variables, what a developer actually needs, and design QA |
| [Usability Evaluation](UI_UX/usability_evaluation.llms.md) | Heuristic evaluation, running a session, writing tasks that do not leak the answer, facilitating without helping, severity rating, and testing with disabled participants |
| [Measurement and Experimentation](UI_UX/measurement_and_experimentation.llms.md) | Event schema design, funnels, session replay and heatmaps, A/B testing and its limits, HEART, Core Web Vitals, SUS and NPS, and the usual statistical traps |
| [Process and Ethics](UI_UX/process_and_ethics.llms.md) | The double diamond, dual-track delivery, design ops, the dark pattern catalogue and why it is now a legal question, consent and privacy, and inclusive design |

------------------------------------------------------------------------

## Skipping the Front End

Python libraries that generate the interface, ordered by how much control they give up.

| Page | Covers |
|----|----|
| [Streamlit](1_streamlit.llms.md) | The most detailed of these. A script becomes a web app, which is why it wins for internal tools |
| [Gradio](2_gradio.llms.md) | The same idea aimed at model demos, an input, an output, and a shareable link |
| [Plotly Dash](3_plotly_dash.llms.md) | Flask, Plotly.js, and React underneath, exposed as Python. More work than Streamlit, more control in return |
| [fastHTML](fasthtml.llms.md) | HTML generated from Python, without the JavaScript layer |
| Grafana | Moved to [IaaS](https://bthek1.github.io/IaaS_docs/Observability/13_Grafana.html), alongside the rest of the observability stack |

------------------------------------------------------------------------

## The Web Platform

| Page | Covers |
|----|----|
| [HTML](html.llms.md) | The markup itself |
| [CSS](css.llms.md) | Styling |
| [Bootstrap](bootstrap.llms.md) | The CSS and JavaScript component framework that saves writing most of it |
| [SVG](svgs.llms.md) | Vector graphics in the browser, at length |
| [Markdown](markdown.llms.md) | The lightweight markup behind most documentation, including this site |
| [HTTP Headers](http_headers.llms.md) | Message headers, how Nginx sets them, and CORS, which is the one that breaks a front end against an API |

------------------------------------------------------------------------

## JavaScript and Its Toolchain

| Page | Covers |
|----|----|
| [JavaScript](Javascript/javascript.llms.md) | Writing the front end against a DRF API |
| [Fetch API](Javascript/fetch_api.llms.md) | Promise-based HTTP requests, replacing XMLHttpRequest |
| [jQuery](Javascript/jquery.llms.md) | The older way, still met in existing code |
| [TypeScript](typescript.llms.md) | Optional static typing over JavaScript, compiling back down to it |
| [Node](node.llms.md) | JavaScript on the server, its core concepts and ecosystem |
| [npm](npm.llms.md) | Dependency management for all of the above |
| [Webpack](webpack.llms.md) | Bundling code, styles, and assets into what the browser actually loads |
| [Prettier](js_prettier.llms.md) | Opinionated formatting across JS, TS, HTML, CSS, and JSON |
| [ESLint](eslint.llms.md) | Linting, for the errors formatting cannot catch |
| [Highcharts](Javascript/highcharts.llms.md) | Charting driven from a DRF endpoint |
| [DataTables](Javascript/datatables.llms.md) | Sortable, searchable tables |
| [SurveyJS](surveyjs.llms.md) | The JSON format for defining forms and surveys |

------------------------------------------------------------------------

## React

| Page | Covers |
|----|----|
| [React Overview](React/react_overview.llms.md) | Fundamentals through to modern patterns and ecosystem tooling |
| [React Setup](React/react_setup.llms.md) | Getting a project running |
| [React Init](React/react_init.llms.md) | The initial scaffold |
| [React Libraries](React/react_libraries.llms.md) | The npm add-ons worth knowing, grouped by what they do |
| [React and Django](React/react_and_django.llms.md) | The full-stack pairing: project structure, how the two halves communicate, deployment, and practice |
| [React with Docker](React/react_docker.llms.md) | A production setup for Django, DRF, React, and PostgreSQL together, using multi-stage builds, Nginx for static files, and Compose to orchestrate it |

------------------------------------------------------------------------

## Flutter

The mobile and desktop route, where one codebase targets Android, iOS, Linux, Windows, and macOS.

| Page | Covers |
|----|----|
| [Flutter Setup](Flutter/flutter_setup.llms.md) | Getting the toolchain working |
| [Widgets](Flutter/widgets.llms.md) | The framework’s whole model is that everything is a widget |
| [Dart](Flutter/dart.llms.md) | The language underneath |
| [Riverpod](Flutter/riverpod.llms.md) | State management |

------------------------------------------------------------------------

## Being Found and Measured

| Page | Covers |
|----|----|
| [SEO](SEO/seo.llms.md) | Split into three layers, of which a full-stack developer owns one completely, shares one, and should refuse the third |
| [Website Metrics](0_website_metrics.llms.md) | Tracking traffic and behaviour through analytics, heatmaps, and log analysis |
| [Google Analytics](1_google_analytics.llms.md) | Wiring GA into a Django project |

------------------------------------------------------------------------

## Not Covered Yet

- **No Vue, Svelte, or Angular.** React is the only JavaScript framework covered.
- **No testing.** Neither component testing nor browser automation appears anywhere.
- **Nothing on state management in React** specifically. Riverpod covers it for Flutter, but Redux, Zustand, and the modern alternatives are absent.
- **Four stubs at two to three cells**: [React Init](React/react_init.llms.md), [Fetch API](Javascript/fetch_api.llms.md), [jQuery](Javascript/jquery.llms.md), and [Google Analytics](1_google_analytics.llms.md).
- **No build-level performance page.** Bundle size and code splitting go unmentioned even though Webpack has a page. Core Web Vitals are covered as a design constraint in [Responsive and Multiplatform](UI_UX/responsive_and_multiplatform.llms.md) and [Measurement and Experimentation](UI_UX/measurement_and_experimentation.llms.md), but not as a build concern.
- **No worked design example.** The design pages are principles and mechanics; none of them takes one screen from research through to built component.

------------------------------------------------------------------------

Back to top
