# Inline Styles that Work

Support for colocating your styles with your React component.

- Supports media queries without user agent sniffing
- Supports pseudo-selectors like :hover, :active, etc. without needing to store 
  hover or active state in components. :visited works just fine too.
- Respects precedence order when specifying multiple styles
- Requires no AST transform (though you can have one to replace 
StyleSheet.create with a pre-computed value at compile time if you'd like).
- Injects only the exact styles needed for the render into the DOM.
- Can be used for server rendering (this is TODO at the moment).
- No dependencies, tiny

# API

    const React, { Component } = require('react');
    const StyleSheet, { css } = require('inline-styles-that-work')

    class App extends Component {
        render() {
            return <div>
                <span className={css([styles.red])}>
                    This should be red.
                </span>,
                <span className={css([styles.hover])}>
                    This should turn red on hover.
                </span>
                <span className={css([styles.small])}>
                    This should turn red when the browser is less than 600px
                    width.
                </span>
                <span className={css([styles.red, styles.blue])}>
                    This should be blue.
                </span>,
                <span className={css([styles.blue, styles.red])}>
                    This should be red.
                </span>,
            </div>;
        }
    }

    const styles = StyleSheet.create({
        red: {
            backgroundColor: 'red'
        },

        blue: {
            backgroundColor: 'blue'
        },

        hover: {
            ":hover": {
                backgroundColor: 'red'
            }
        },

        small: {
            "@media (max-width: 600px)": {
                backgroundColor: "red",
            }
        }
    });

# TODO

- Examples in the repo
- Autoprefixing
- Batch styles in a single render cycle into a single style tag
- Serverside rendering
- Optional AST transformation to replace StyleSheet.create with an object 
literal.
- Add Flow annotations
- Automatic conversion of numbers to strings for properties where we know what 
  the unit is. See CSSProperty.js in React.

# Other solutions

- [js-next/react-style](https://github.com/js-next/react-style)
- [dowjones/react-inline-style](https://github.com/dowjones/react-inline-style)
- [martinandert/react-inline](https://github.com/martinandert/react-inline)
