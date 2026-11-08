# Change Log

All notable changes to the "neo-lang" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [0.0.4]

- Read-only pointer types `^const T`, `[^]const T` and `[..]const T`: the
  `const` highlights as a keyword and the type after it keeps its type color.
  Previously the `const name` declaration rule took the type for a variable
  name, so `^const int` colored `int` as a variable.

## [0.0.3]

Synced to the current compiler (v0.0.140-dev) and spec:

- `namespace foo;` declarations replaced by the `#namespace foo;` directive
  (new `namespace_decl` rule; the old `namespace` keyword rule is gone —
  `namespace` is a plain identifier now). Bare `#namespace` in expression
  position is still highlighted as a location macro.
- Tests are `#test("name") { }` / `#test { }` with `#[skip]`; removed the
  stale `test "name"` / `skip test` keyword rules and added `#test` (with its
  name capture), `#no_context`, and `#c_varargs` to the directives.
- `#import <ns>` / `#import <ns::sub>` angle-bracket stdlib paths are now
  recognized in all import forms (previously only bare and quoted paths).
- `new`/`free` demoted from keywords to builtin functions (they are runtime
  generics since 2026-06-17); added `pop`, `remove`, `remove_unordered`, and
  the `*_safe` allocation variants to the builtin list.
- Added the missing `bool` primitive; `context` is highlighted as a language
  variable (the implicit `^Neo_Context`).
- Float literals: added the `12.f` / `100.d` dot-suffix form.
- Removed C-style `/* */` block-comment rules: the lexer and spec only define
  `//` and nested `/- -/`.
- Bare `fn` now highlights in function-pointer types and lambdas
  (`alloc_fn: fn(^Allocator): rawptr`, `fn(): int { ... }`) — previously only
  `fn name(...)` forms were colored.
- Enum shorthand `.Variant` highlights as an enum member (dot not preceded by
  a value expression, so `foo.bar`, `p^.field`, and `t.0` are unaffected).
- Added `type_assert` to the intrinsics.
- `name!(...)` calls to `#[__global]` runtime functions (`assert!`, `panic!`,
  `append!`, `new!`, `make!`, ...) highlight as builtin functions, `!`
  included. Primitive and capitalized names are skipped so Result types like
  `string!(E)` are unaffected. The bare runtime names (`new`, `free`, `make`,
  `delete`, `append`, `pop`, `remove`, `remove_unordered`) are no longer
  highlighted as builtins, since a plain call to them is now a user function.

## [0.0.2]

Grammar synced to the current Neo language (lexer + spec):

- Block comments support both the nested `/- -/` form and C-style `/* */`
  (including `/** */` doc and `/*: */` playground variants), which Neo will support.
- Trimmed intrinsic keywords to those the lexer actually recognizes
  (`cast`, `recast`, `auto_cast`, `type_of`, `typename_of`, `typeid_of`,
  `typeinfo_of`, `size_of`, `align_of`); memory keywords reduced to `new`/`free`.
- Reflection/introspection and container helpers (`is_*`, `fields_of`, `enum_*`,
  `soa_*`, `make`, `append`, `len`, `cap`, …) are now highlighted as builtin
  functions rather than keywords.
- Added keywords/types: `api`, `volatile`, `unreachable`, `b1`, `isize`, `usize`,
  `Result`, `Optional`.
- Removed `distinct`, `Self`, `unused` (no longer keywords; `distinct` is the
  `#[distinct]` attribute).
- Added operators: `**`, `||=`, `<-`, `@@`, `?.`, `.!`, and saturating `@<<`/`@<<=`.
- Numeric literals now support exponents (`1.5e-9`), the full float-suffix set
  (`f F d D h H q Q`), and base-4 `0q` literals.
- Added the `#context_append` directive.

## [Unreleased]

- Initial release
