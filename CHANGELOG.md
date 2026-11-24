# Changelog

## 5.0.0

Fork of `diablomedia/zendframework1-test`, published as `gizmocraft/zendframework1-test`.

### Breaking changes

- Requires PHP `>=8.5`. Tested on PHP 8.5 and 8.6.
- Package renamed from `diablomedia/zendframework1-test` to `gizmocraft/zendframework1-test`. It now requires the `gizmocraft/zendframework1-*` packages `exception`, `loader`, `registry`, `controller`, `application`, `db`, `dom`, `filter` and `layout` (each `^2.0.0`) and `session` (`^3.0.0`). Dev dependencies: `controller-action-helper-json` and `dojo` (`^2.0.0`).

### Supported PHPUnit versions

- `phpunit/phpunit` is now `^10.5 || ^11.5 || ^12.5 || ^13.0` (upstream: `^10.5.0`) and `sebastian/comparator` is `^5.0.1 || ^6.0 || ^7.0 || ^8.0` (upstream: `^5.0.1`). The full test suite (80 tests, no skips) passes on PHP 8.5 and 8.6 against the lowest and the highest installable release of each PHPUnit major: 10.5.x, 11.5.x, 12.5.x and 13.x (13.0.0 and 13.4.8).
- No library change was needed for PHPUnit 11, 12 or 13: the constraints (`Zend_Test_PHPUnit_Constraint_DomQuery`, `Redirect`, `ResponseHeader`) and `Zend_Test_PHPUnit_ControllerTestCase` already use the PHPUnit 10 API (`evaluate(): ?bool`, `fail(): never`, `toString(): string`, `setUp(): void`, `addToAssertionCount()`), which PHPUnit 11 to 13 keep. The package does not use `PHPUnit\Extensions\Database`, `getMockBuilder()` or `$this->any()`.
- `Zend_Test_PHPUnit_Constraint_Exception` still extends `Exception` (as in upstream 4.0.1), so a failed `assertQuery()`/`assertRedirect()`/`assertHeader()` is reported by PHPUnit as an error, not as a failure.

### Other changes

- No `src` changes and no public signature changes compared to upstream 4.0.1.
- Dev dependencies upgraded (PHPUnit 13, PHPStan 2.3, php-cs-fixer 3.95, GrumPHP 2.27). Dropped `composer-require-checker`, which has no release for PHP 8.6.
- Tests migrated to PHPUnit 13 attributes (`#[Group]`, `#[DataProvider]`, `#[DoesNotPerformAssertions]`). Before, PHPUnit 12 and 13 ignored the docblock annotations, which made two data provider tests fail with `ArgumentCountError`. The skipped test `testAssertionsShouldIncreasePhpUnitAssertionCounter` now runs, using `numberOfAssertionsPerformed()`.
- CI runs PHP 8.5 and 8.6.
