> **Rust Edition Guide は現在 Rust 2024 のアップデート作業に向けて翻訳作業中です。本ページは英語版をコピーしていますが、一部のリンクが動作しないなどの問題が発生する場合があります。問題が発生した場合は、[原文（英語版）](https://doc.rust-lang.org/nightly/edition-guide/introduction.html)をご参照ください。**

# Rustfmt: Combine all delimited exprs as last argument

## Summary

* Some expressions with multi-line final arguments will now format as a single line, with the final expression overflowing.

## Details

When structs, slices, arrays, and block/array-like macros are used as the last argument in an expression list, they are now allowed to overflow (like blocks/closures) instead of being indented on a new line.

```rust,ignore
// Edition 2021

fn example() {
    foo(ctx, |param| {
        action();
        foo(param)
    });

    foo(
        ctx,
        Bar {
            x: value,
            y: value2,
        },
    );

    foo(
        ctx,
        &[
            MAROON_TOMATOES,
            PURPLE_POTATOES,
            ORGANE_ORANGES,
            GREEN_PEARS,
            RED_APPLES,
        ],
    );

    foo(
        ctx,
        vec![
            MAROON_TOMATOES,
            PURPLE_POTATOES,
            ORGANE_ORANGES,
            GREEN_PEARS,
            RED_APPLES,
        ],
    );
}
```

This now formats as the following in the 2024 style edition:

```rust,ignore
// Edition 2024

fn example() {
    foo(ctx, |param| {
        action();
        foo(param)
    });

    foo(ctx, Bar {
        x: value,
        y: value2,
    });

    foo(ctx, &[
        MAROON_TOMATOES,
        PURPLE_POTATOES,
        ORGANE_ORANGES,
        GREEN_PEARS,
        RED_APPLES,
    ]);

    foo(ctx, vec![
        MAROON_TOMATOES,
        PURPLE_POTATOES,
        ORGANE_ORANGES,
        GREEN_PEARS,
        RED_APPLES,
    ]);
}
```

## Migration

The change can be applied automatically by running `cargo fmt` or `rustfmt` with the 2024 Edition. See the [Style edition] chapter for more information on migrating and how style editions work.

[Style edition]: rustfmt-style-edition.md
