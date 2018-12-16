# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [Unreleased]
### Added
- Implement `FuzzyEq` for `Rect`, `Size` and `Point`.
- `StrokeMiterlimit` and `FontSize` wrappers for `f64`.

### Changed
- Shapes without fill and stroke will no longer be removed.
- `FilterPrimitive::filter_input` was removed and each filter primitive that can
  have an input has it's own `filter_input` field now.
- Rename `filter_input` fields into `input`.
- Filter primitives inputs and results will be resolved now.

### Fixed
- `offset` attribute resolving inside the `stop` element.

### Removed
- `Rect::transform`.

## [0.4.0] - 2018-12-13
### Added
- Initial [Basic Filters](http://www.w3.org/TR/SVG11/feature#BasicFilter) support.
- Nested `clipPath` support.
- `systemLanguage` attribute support.
- `mask` attribute on `mask` element support.
- Default font family and size is configurable now.
- `StrokeWidth` wrapper.
- `ClipPath::clip_path`.
- `visibility` field for `Path`, `TextSpan` and `Image`.
- Most of the structs are implement Clone and Debug now.

### Changed
- `Opacity` and `StopOffset` will be clamped to the 0..1 range now.
- The `visibility` attribute will not be removed now,
  because invisible elements still impact the bbox calculation.
- Elements with zero opacity will not be removed now,
  because such elements still impact the bbox calculation.
- No `PartialEq` for `Line`, `Point`, `Size` and `Rect`. Because of `f64`.

### Fixed
- `display` attribute processing.
- Recursive `mask` resolving.
- `inherit` attribute value resolving.
- Complex style resolving.

## [0.3.0] - 2018-09-12
### Added
- Implement `Deref` for `LinearGradient` and `RadialGradient`.
- (cli) `--indent` and `--attrs-indent` flags.
- (cli) Use `gumdrop` instead of `getopts`.
- `Error::ParsingFailed`.

### Changed
- Gradient stops are stored directly in the `BaseGradient` and not as `NodeKind::Stop` now.
- `TextChunk` are stored directly in the `Text` and not as `NodeKind::TextChunk` now.
- Rename `LinearGradient::d` to `LinearGradient::base`.
- Rename `RadialGradient::d` to `RadialGradient::base`.
- Rename `TSpan` to `TextSpan`.
- `Tree::from_str` will return a `Result` now.

### Removed
- `failure` dependency.

## [0.2.0] - 2018-05-23
### Added
- Remove elements with `opacity="0"`.
- Transfer the group `id` attribute to the child when group has only one child.
- `symbol` element support.
- `Tree::from_str`.
- Nested `svg` elements support.
- SVG support for `image` element.
- `ImageFormat::SVG`.
- `Image::format`.
- Paint fallback resolving.
- Bbox validation for shapes that use painting servers.
- `TextChunk::dx` and `TextChunk::dy`.
- `Text::rotate`.
- `rotate` attribute processing.

### Changed
- `tree` module content reexported.
- `parse_tree_from_*` methods move to the `Tree`. Use `Tree::from_*` instead.
- Rename `Tree::node_by_svg_id` to `Tree::node_by_id`.
- Use `rctree::Node<NodeKind>` instead of `rctree::Node<Box<NodeKind>>`.
- `view` element is out of scope now.
- `FileReadError` replaced with `Error`.
- `parse_tree_from_data` accepts `&[u8]` and not `&str` now.
- Rename `ImageDataKind` to `ImageFormat`.
- New geometry primitives implementation.
- `TextChunk::x` and `TextChunk::y` are `Option<NumberList>` and not `f64` now.

### Removed
- `NodeExt::kind`. Use `Node::borrow` instead.

### Fixed
- Panic during `visibility` resolving.
- Gradients with one stop resolving.
- `use` attributes resolving.
- `clipPath` and `mask` attributes resolving.
- `offset` attribute in `stop` element resolving.
- Incorrect `font-size` attribute resolving.
- Gradient stops resolving.
- `switch` element resolving.

[Unreleased]: https://github.com/RazrFalcon/usvg/compare/v0.4.0...HEAD
[0.4.0]: https://github.com/RazrFalcon/usvg/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/RazrFalcon/usvg/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/RazrFalcon/usvg/compare/v0.1.1...v0.2.0