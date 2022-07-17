## Markdown
This is _italic_ or *italic*, **bold** or __bold__, ***bold italic*** or ___bold italic___,
~~striked~~ and *~~striked~~* and **~~striked~~**. As far as we know, Markdown
==highlights== are not parsed.

## Vector shorthands

We provide three different vector styles:

-   `\ArrowVector` $\ArrowVector{a}$ and $\ArrowVector{x_{123}}$, using the `\vv` command from `esvect`;
-   `\LongVector` $\LongVector{a}$ and $\LongVector{x_{123}}$, using `\overrightarrow`;
-   `\BoldVector` $\BoldVector{a}$ and $\BoldVector{x_{123}}$, using `\mathbf` or `\symbf`.

Each document should have the `\vec` command re-set to one of these:
usually we do not want to mix them and it is nice to have a global style.
In this document, `\vec{a}` is rendered as $\vec{a}$.

### Common operators
Gradient, divergence and rotation operators have their own shorthands, including auto-vectorizing ones:
```
$${
    \Grad{\vec{v}} &= \GradV{v} &= \GradT{\vec{v}} &= \GradTV{v} \\
    \Div{\vec{v}} &= \DivV{v} &= \DivT{\vec{v}} &= \DivTV{v} \\
    \Rot{\vec{v}} &= \RotV{v} &= \RotT{\vec{v}} &= \RotTV{v} \\
}$$
```
$${
    \Grad{\vec{v}} &= \GradV{v} &= \GradT{\vec{v}} &= \GradTV{v} \\
    \Div{\vec{v}} &= \DivV{v} &= \DivT{\vec{v}} &= \DivTV{v} \\
    \Rot{\vec{v}} &= \RotV{v} &= \RotT{\vec{v}} &= \RotTV{v} \\
}$$

## Derivatives
Derivatives are to be written with the `\*Derivative*` class shorthands.
For brevity, all `\Derivative`-class shorthands can be written with `Drv` instead.

### Simple derivative
The simplest use case is a univariate derivative, possibly of higher order.
This is conveniently written as `\Derivative[order]{dependent}{independent}`, for instance
```
$$
    \Derivative{f}{x} < \Derivative[2]{g}{x} = \DrvE{x} \Drv{g}{x}
$$
```
$$
    \Derivative{f}{x} < \Derivative[2]{g}{x} = \DrvE{x} \Drv{g}{x}
$$

### Empty derivative {#emptyd}
If the dependent is a complicated expression, it is customary to write
it _after_ the derivative. This is done with the help of `\DerivativeEmpty`.
The order of the arguments is reversed so that it matches the usual order
```
$$
    \DerivativeEmpty[5]{x} f(x) = \DrvE[5]{x} f(x)
$$
```
$$
    \DerivativeEmpty[5]{x} f(x) = \DrvE[5]{x} f(x)
$$

### Parenthesised derivative
Similar to [empty derivatives](#emptyd), DeGeŠ provides a parenthesised empty derivative
```
$$
    \DerivativeParen[2]{x^3 - x^2 + 1}{x} = \DrvP[2]{x^3 - x^2 + 8}{x}
$$
```
$$
    \DerivativeParen[2]{x^3 - x^2 + 1}{x} = \DrvP[2]{x^3 - x^2 + 8}{x}
$$

### Partial derivatives and finite differences
Changing the differential can be achieved by prepending a letter:
`P` for partial derivatives ($\pdiff$), `F` for finite differences ($\fdiff$)
or `U` for functional differences ($\udiff$). All combinations of prefixes and postfixes are allowed.
Internally, this is all achieved by a single command and only the differential symbol is varied.
```
$$
    \PDerivativeEmpty[2]{x}{f(x, y, z)} = \PDrvE[2]{x}{f(x, y, z)}
    \approx \FDrvE[2]{z}{f(x, y, z)} \neq \UDrvE[3]{f(x)}{}
$$
```
$$
    \PDerivativeEmpty[2]{x}{f(x, y, z)} = \PDrvE[2]{x}{f(x, y, z)}
    \approx \FDrvE[2]{z}{f(x, y, z)} \neq \UDrvE[3]{f(x)}
$$

## Integrals
Integrals are to be written using the `\Int*` shorthand class, which adds
spaces, limits and variables automatically.
The most generic template is `\Int[lower][upper]{integrand}{variable}`.
Compare this with the standard `\int\limits_{lower}^{upper} integrand\,\mathrm{d}\!{variable}`.

Simple indefinite integral is
```
$$
    \Int{x}{x} \QText{or} \Int{\left(x^2 + x + \ln x\right)}{x}
$$
```
$$
    \Int{x}{x} \QText{or} \Int{\left(x^2 + x + \ln x\right)}{x}
$$

If integration limits are supplied they are rendered as
```
$$
    \Int[0][1]{x}{x}
$$
```
$$
    \Int[0][1]{x}{x}
$$
or inline as $\Int[0][1]{x}{x}$.

### Dot and cross product integrals
Sometimes a dot or cross product of the integrand and the variable is needed.
This can be easily achieved with `\IntD` and `\IntC` respectively, or their `*V`
variants which automatically turn arguments into vectors:
```
    \IntD[\ell]{\vec{E}}{\vec{x}} \QText{and} \IntDV[\pdiff\Omega]{B}{l},
    \IntC[\ell]{\vec{G}}{\vec{y}} \QText{and} \IntCV[\pdiff\Omega]{W}{s}
```
$$
    \IntD[\ell]{\vec{E}}{\vec{x}} \QText{and} \IntDV[\pdiff\Omega]{B}{l},
    \IntC[\ell]{\vec{G}}{\vec{y}} \QText{and} \IntCV[\pdiff\Omega]{W}{s}
$$

### Closed curve integral
Use `\OIntD[domain]{integrand}{variable}` for dot product,
or `\OIntDV[domain]{integrand}{variable}` as a vector shorthand:
```
$$
    \OIntD{\left(\vec{c} \times \vec{d}\right)}{\vec{u}} \QText{and} \OIntDV[\ell]{B}{l} = 0
$$
```
$$
    \OIntD{\left(\vec{c} \times \vec{d}\right)}{\vec{u}} \QText{and} \OIntDV[\ell]{B}{l} = 0
$$

### Two-dimensional integral
This notation extends to higher dimensions, with two-dimensional integral with two
differentials being written as
```
$$
    \IInt[0, 0][1, 1]{5x^2 - y^3}{x}{y}
$$
```
$$
    \IInt[0, 0][1, 1]{5x^2 - y^3}{x}{y}
$$

If only a single differential is desired, the `I` version does just that:
```
$$
    \IIntI[\vec{S}]{\left(x + y\right)}{\vec{S}}
$$
```
$$
    \IIntI[\vec{S}]{\left(x + y\right)}{\vec{S}}
$$

$$
    \Abs{\PDrv{y}{x}}
$$

