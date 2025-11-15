# Odoo CSS: Core vs Plugin Breakdown

**Date:** 2025-11-15
**Purpose:** Clarify the distinction between Core CSS and Plugin/Addon CSS in Odoo

---

## Important Clarification

In Odoo's architecture, **Core CSS is located in the `/addons/web/` module**. This might be confusing because it's in an "addons" directory, but `/addons/web/` IS the core web framework that everything else builds upon.

---

## Core CSS (Web Module)

**Location:** `/home/user/odoo/addons/web/static/src/`

### Core SCSS Foundation Files

The web module contains **3,190 lines of core SCSS** in the `/scss/` directory alone:

| File | Lines | Purpose |
|------|-------|---------|
| `primary_variables.scss` | 297 | **Main design tokens** - colors, typography, spacing |
| `secondary_variables.scss` | 51 | Additional UI variables (colors, spacing) |
| `bootstrap_overridden.scss` | 315 | Bootstrap 5 customizations |
| `bootstrap_review_backend.scss` | 326 | Backend-specific Bootstrap overrides |
| `bootstrap_review_frontend.scss` | 348 | Frontend-specific Bootstrap overrides |
| `utils.scss` | 411 | **Utility mixins & functions** |
| `utilities_custom.scss` | 208 | Custom utility classes |
| `bootstrap_review.scss` | 133 | General Bootstrap review/fixes |
| `ui.scss` | 199 | Core UI components styling |
| `fontawesome_overridden.scss` | 112 | Icon system customizations |
| `bs_mixins_overrides.scss` | 96 | Bootstrap mixin overrides |
| `pre_variables.scss` | 82 | Pre-processing variables |
| `mimetypes.scss` | 73 | File type icons |
| `import_bootstrap.scss` | 67 | Bootstrap import orchestration |
| `functions.scss` | 51 | SCSS helper functions |
| Others | 421 | Animation, base layouts, etc. |
| **TOTAL** | **3,190** | **Core styling foundation** |

### Core Component Styles

The web module contains **100+ component SCSS files** in organized directories:

```
/addons/web/static/src/
├── core/                           # 60+ core UI components
│   ├── avatar/avatar.scss
│   ├── autocomplete/autocomplete.scss
│   ├── badge/badge.scss
│   ├── barcode/barcode_dialog.scss
│   ├── bottom_sheet/bottom_sheet.scss
│   ├── checkbox/checkbox.scss
│   ├── color_picker/color_picker.scss
│   ├── colorlist/colorlist.scss
│   ├── commands/command_palette.scss
│   ├── datetime/datetime_picker.scss
│   ├── debug/debug_menu.scss
│   ├── dialog/dialog.scss
│   ├── dropdown/dropdown.scss
│   ├── dropzone/dropzone.scss
│   ├── emoji_picker/emoji_picker.scss
│   ├── errors/error_dialog.scss
│   ├── file_upload/file_upload_progress_bar.scss
│   ├── file_viewer/file_viewer.scss
│   ├── hotkeys/hotkey_dialog.scss
│   ├── l10n/l10n.scss
│   ├── menu_items/menu_items.scss
│   ├── model_field_selector/model_field_selector.scss
│   ├── name_and_signature/name_and_signature.scss
│   ├── notebook/notebook.scss
│   ├── notifications/notification_container.scss
│   ├── overlay/overlay.scss
│   ├── pager/pager.scss
│   ├── popover/popover.scss
│   ├── radio/radio.scss
│   ├── rating/rating.scss
│   ├── record_selectors/record_selector.scss
│   ├── resizable_panel/resizable_panel.scss
│   ├── signature/signature.scss
│   ├── sortable_list/sortable_list.scss
│   ├── stripes/stripes.scss
│   ├── tags/tags.scss
│   ├── tree_editor/tree_editor.scss
│   └── ... (30+ more)
│
├── views/                          # 25+ view-specific styles
│   ├── activity/activity_renderer.scss
│   ├── calendar/calendar_renderer.scss
│   ├── card/card_compiler.scss
│   ├── fields/
│   │   ├── field.scss
│   │   ├── boolean_field/boolean_field.scss
│   │   ├── char_field/char_field.scss
│   │   ├── date_field/date_field.scss
│   │   ├── image_field/image_field.scss
│   │   ├── many2many_field/many2many_field.scss
│   │   └── ... (40+ field types)
│   ├── form/
│   │   ├── form_controller.scss
│   │   ├── form_label.scss
│   │   ├── button_box/button_box.scss
│   │   └── status_bar/status_bar.scss
│   ├── kanban/
│   │   ├── kanban_renderer.scss
│   │   ├── kanban_record.scss
│   │   └── kanban_header.scss
│   ├── list/
│   │   ├── list_renderer.scss
│   │   └── editable_list_renderer.scss
│   └── graph/graph_renderer.scss
│
├── webclient/                      # 25+ webclient UI styles
│   ├── actions/
│   │   ├── action_dialog.scss
│   │   └── reports/report.scss
│   ├── burger_menu/burger_menu.scss
│   ├── debug/profiling/profiling_item.scss
│   ├── icons.scss
│   ├── loading_indicator/loading_indicator.scss
│   ├── navbar/navbar.scss
│   ├── settings_form_view/settings_form_view.scss
│   ├── switch_company_menu/switch_company_menu.scss
│   ├── user_menu/user_menu.scss
│   ├── webclient_layout.scss
│   └── webclient.scss
│
└── scss/                           # Foundation (covered above)
    └── ... (24 files, 3,190 lines)
```

### Core JavaScript Files with Dynamic Styling

**Location:** `/addons/web/static/src/core/`

These JavaScript files dynamically manipulate CSS:

| File | Purpose |
|------|---------|
| `utils/colors.js` | RGB↔HSL conversion, color mixing, blending |
| `colors/colors.js` | Predefined color palettes (SM/MD/LG/XL) |
| `bottom_sheet/bottom_sheet.js` | Dynamic `--sheet-height` CSS variable |
| `barcode/crop_overlay.js` | Dynamic `--o-crop-x`, `--o-crop-y` positioning |
| `resizable_panel/resizable_panel_hook.js` | Dynamic panel width manipulation |
| `draggable/draggable_hook_builder.js` | Dynamic element positioning |

### Core Asset Bundles

**Location:** `/addons/web/__manifest__.py`

The web module defines all core asset bundles:

```python
'assets': {
    # Core bundles
    'web.assets_backend',           # Main backend interface
    'web.assets_frontend',          # Main frontend/website
    'web.assets_web',              # Full web client
    'web.assets_web_dark',         # Dark mode theme

    # Helper bundles
    'web._assets_primary_variables',    # Primary design tokens
    'web._assets_secondary_variables',  # Secondary tokens
    'web._assets_bootstrap',            # Bootstrap compilation
    'web._assets_helpers',              # Mixins/functions

    # Specialized bundles
    'web.report_assets_common',    # Report styling
    'web.report_assets_pdf',       # PDF report styling
    'web.assets_web_print',        # Print styling
}
```

---

## Plugin/Addon CSS

**Location:** `/home/user/odoo/addons/[addon_name]/static/src/`

Plugins extend the core with their own styles. Examples:

### Example 1: Account (Accounting Module)

```
/addons/account/static/src/
├── scss/
│   ├── variables.scss              # Overrides core variables
│   ├── account.scss                # Main accounting styles
│   ├── account_journal_dashboard.scss
│   ├── account_move_send_wizard.scss
│   ├── account_payment_term.scss
│   └── ... (8 more files)
├── components/
│   ├── account_file_uploader/account_file_uploader.scss
│   ├── bill_guide/bill_guide.scss
│   ├── tax_totals/tax_totals.css
│   └── ... (6 more components)
└── css/
    ├── account.css
    ├── account_bank_and_cash.css
    ├── report_invoice.css
    └── account_payment.scss
```

**Plugin manifest:** `/addons/account/__manifest__.py`

```python
'assets': {
    'web._assets_primary_variables': [
        'account/static/src/scss/variables.scss',  # Extend core variables
    ],
    'web.assets_backend': [
        'account/static/src/css/account.css',      # Add to core bundle
        'account/static/src/scss/account.scss',
        'account/static/src/components/**/*',      # All components
    ],
}
```

### Example 2: Website (Website Builder Module)

```
/addons/website/static/src/
├── scss/
│   ├── user_custom_bootstrap_overridden.scss
│   ├── user_custom_variables.scss
│   └── website.scss
├── snippets/                       # 50+ snippet styles
│   ├── s_announcement/announcement.scss
│   ├── s_banner/banner.scss
│   ├── s_carousel/carousel.scss
│   └── ... (50+ more)
├── interactions/
│   ├── cookies/cookies.scss
│   ├── full_screen_height.scss
│   └── header/header.scss
└── components/
    └── ... (various components)
```

### Example 3: HR (Human Resources)

```
/addons/hr/static/src/
├── scss/
│   └── hr.scss
└── components/
    ├── avatar_card/avatar_card.scss
    └── employee_chat/employee_chat.scss
```

---

## How Plugins Extend Core CSS

### Method 1: Variable Override

Plugins can override core variables by adding to the `web._assets_primary_variables` bundle:

```scss
// Plugin: account/static/src/scss/variables.scss
$o-brand-primary: #017e84 !default;  // Override default purple
$o-enterprise-action-color: #017e84 !default;
```

### Method 2: Component Extension

Plugins add their own component styles that build on core components:

```scss
// Plugin: account/static/src/scss/account.scss
.o_account_dashboard {
    // Extends core .o_kanban_view styling
    .o_kanban_record {
        // Uses core border-radius, shadows, etc.
        border-radius: $o-border-radius;
        box-shadow: 0 1px 3px rgba(0,0,0,0.12);
    }
}
```

### Method 3: Bundle Insertion

Plugins can insert styles at specific points:

```python
'web.assets_backend': [
    ('after', 'web/static/src/scss/primary_variables.scss',
     'my_addon/static/src/scss/custom_variables.scss'),
]
```

---

## Key Differences: Core vs Plugin

| Aspect | Core (web module) | Plugins (other modules) |
|--------|-------------------|-------------------------|
| **Location** | `/addons/web/` | `/addons/[name]/` |
| **Purpose** | Foundation & framework | Feature-specific styling |
| **Scope** | Universal (all views) | Module-specific |
| **Variables** | Define design tokens | Override/extend tokens |
| **Components** | Base UI components | Feature components |
| **Bootstrap** | Customizes BS5 | Uses customized BS5 |
| **Bundles** | Defines core bundles | Extends core bundles |
| **Lines of SCSS** | 3,190+ (just /scss/) | Varies (50-500 typically) |
| **Total Files** | 100+ SCSS files | 5-50 SCSS files typically |

---

## Statistics Summary

### Core CSS (Web Module)

- **Foundation SCSS:** 3,190 lines (24 files in `/scss/`)
- **Component SCSS:** 100+ files in `/core/`, `/views/`, `/webclient/`
- **Total Core CSS/SCSS:** Approximately **8,000-10,000 lines**
- **Bootstrap Library:** Included (customized BS5)
- **Icon Library:** Font Awesome 4.7
- **Dark Mode Files:** 23+ `.dark.scss` files

### Plugin CSS (All Other Modules)

- **Number of Modules with CSS:** 294+ modules
- **Total Plugin CSS:** Approximately **50,000-60,000 lines** across all plugins
- **Average per Plugin:** 50-500 lines (varies widely)
- **Total CSS/SCSS in Odoo:** 1,119+ files

---

## What the Original Analysis Covered

The document `ODOO_CSS_ANALYSIS_AND_UNTITLEDUI_RECOMMENDATIONS.md` **DID analyze Core CSS**, specifically:

### Core Files Analyzed:

1. ✅ `/addons/web/static/src/scss/primary_variables.scss` (297 lines)
2. ✅ `/addons/web/static/src/scss/secondary_variables.scss` (51 lines)
3. ✅ `/addons/web/static/src/scss/bootstrap_overridden.scss` (315 lines)
4. ✅ `/addons/web/static/lib/bootstrap/scss/_variables.scss` (Bootstrap core)
5. ✅ `/addons/web/static/src/scss/utils.scss` (411 lines)
6. ✅ `/addons/web/static/src/core/utils/colors.js` (484 lines)
7. ✅ `/addons/web/static/src/core/colors/colors.js` (218 lines)
8. ✅ `/addons/web/static/src/webclient/navbar/navbar.scss`
9. ✅ `/addons/web/static/src/views/form/button_box/button_box.scss`
10. ✅ Asset bundle system (`assetsbundle.py`, `ir_asset.py`)

### What Might Have Been Confusing:

- The term "addons" includes both core (`/addons/web/`) and plugins
- The document focused on the *architecture* (how CSS works) rather than listing every file
- Examples used both core and plugin files without clear labels

---

## Recommendations for Core CSS Improvements

Based on the analysis, here are the **Core CSS files that should be modified** to implement UntitledUI styling:

### Phase 1: Update Core Variables

**File:** `/addons/web/static/src/scss/untitled_ui_variables.scss` (NEW)

Create this new file with modern design tokens (as detailed in the main analysis document).

**File:** `/addons/web/static/src/scss/primary_variables.scss` (UPDATE)

Update these existing variables:
```scss
// Current → Recommended
$o-border-radius: 4px → 8px
$o-border-radius-sm: 3px → 4px
$o-border-radius-lg: 6px → 12px

$o-font-size-base: 14px → 16px (optional, breaking)
```

### Phase 2: Update Core Components

**Files to modify:**

1. `/addons/web/static/src/core/dialog/dialog.scss` - Add shadows, modern radius
2. `/addons/web/static/src/core/dropdown/dropdown.scss` - Better shadows
3. `/addons/web/static/src/core/autocomplete/autocomplete.scss` - Modern styling
4. `/addons/web/static/src/core/notebook/notebook.scss` - Better tabs
5. `/addons/web/static/src/views/form/form_label.scss` - Typography updates
6. `/addons/web/static/src/views/form/button_box/button_box.scss` - Modern buttons
7. `/addons/web/static/src/webclient/navbar/navbar.scss` - Better navigation
8. `/addons/web/static/src/scss/bootstrap_overridden.scss` - Button/form overrides

### Phase 3: Update Core Utilities

**File:** `/addons/web/static/src/scss/utilities_custom.scss`

Add new utility classes:
```scss
// Shadow utilities
.shadow-xs { box-shadow: $o-shadow-xs; }
.shadow-sm { box-shadow: $o-shadow-sm; }
// ... etc

// Spacing utilities (8px grid)
.p-1 { padding: $o-space-1; }  // 4px
.p-2 { padding: $o-space-2; }  // 8px
// ... etc
```

---

## Conclusion

**YES, there is extensive Core CSS in Odoo!**

- **Core CSS** is in `/addons/web/` (3,190+ lines of foundation SCSS + 100+ component files)
- **Plugin CSS** is in `/addons/[other_modules]/` (50,000+ lines total across 294 modules)
- The original analysis **DID cover Core CSS** extensively
- Most UX improvements should focus on **updating Core files** in `/addons/web/`

To improve Odoo's UX with UntitledUI styling, you should primarily modify:
1. Core variable files (`primary_variables.scss`, new `untitled_ui_variables.scss`)
2. Core component styles (dialog, dropdown, forms, buttons, etc.)
3. Core Bootstrap overrides (`bootstrap_overridden.scss`)
4. Core utilities (`utilities_custom.scss`)

Plugin CSS will automatically benefit from core improvements since plugins inherit core variables and components.

---

**Questions?** Let me know if you need more details about specific Core CSS files or how they relate to the UntitledUI recommendations!
