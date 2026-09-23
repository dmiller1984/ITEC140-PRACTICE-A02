# PRACTICE ONLY — Concession Register Tax Toggle

**Dalton Miller · ITEC 140 · Independent practice · Not for submission**

This is an ungraded Windows Forms exercise. It uses the same general screen arrangement as the class concession-register exercise so the Designer work feels familiar, but it adds Dalton's separate tax experiment:

- store both practice tax rates at Form/field scope;
- calculate both tax results in the same `Total Tax` Click event;
- display the 5% result first;
- use one Boolean field and logical NOT (`!`) to alternate the visible result on later clicks;
- keep the two sets of results in the same location so the Form still looks like one register.

The rates are hypothetical programming values. They are not a statement of current Canadian or Quebec tax law.

> [!IMPORTANT]
> This repository is labelled **PRACTICE ONLY**. Do not copy it into a graded repository or submit it. The real class assignment prohibits AI assistance. For the real assignment, use Richard's instructions, your notes, and tutor-style questions or explanations only; write every line yourself.

## What is supplied

The repository contains a blank .NET 10 Windows Forms starter. The calculation and event-handler code are intentionally not completed. You will place the controls, create the event handlers, write each statement, and test it yourself.

## Part 1 — Open the practice starter

1. On this repository page, select **Code** and copy the HTTPS clone address.
2. In Visual Studio, choose **Clone a repository**, paste the address, and select **Clone**.
3. Open `ITEC140-PRACTICE-A02.sln` if Visual Studio shows a folder view.
4. In Solution Explorer, right-click `Form1.cs` and choose **View Designer**.
5. Press **F5** once. A blank Form titled **PRACTICE ONLY - Concession Register Tax Toggle** is expected.
6. Close the running Form before editing it.
7. Open **View > Toolbox**. Select a control and press **F4** to open Properties.

Use Windows with the **.NET desktop development** workload and .NET 10 SDK. `(Name)` is the identifier used by C#; `Text` is the wording visible on the Form.

## Part 2 — Recreate the reference arrangement

Use the wireframe in [`docs/PRACTICE-LAYOUT.svg`](docs/PRACTICE-LAYOUT.svg). It is an original practice drawing, not Richard's private screenshot.

Arrange the Form like this:

- four food rows on the left, with two items per row;
- each item name above its price button;
- one large receipt ListBox on the right;
- the `Total` and `Total Tax` buttons below the ListBox;
- the ordinary total to the right of `Total`;
- the tax and complete total to the right of `Total Tax`;
- two result panels occupying the same location, with only one visible at a time.

Set the Form's `Text` property to `PRACTICE ONLY - Concession Register Tax Toggle` so it can never be mistaken for the graded project.

### Base register controls

Create these controls in the Designer before writing event code.

| Control | `(Name)` | `Text` / setting |
|---|---|---|
| Label | `lblPizza` | `Pizza` |
| Button | `btnPizza` | `$1.99` |
| Label | `lblSalad` | `Salad` |
| Button | `btnSalad` | `$2.99` |
| Label | `lblCoffee` | `Coffee` |
| Button | `btnCoffee` | `$1.99` |
| Label | `lblLatte` | `Latte` |
| Button | `btnLatte` | `$5.99` |
| Label | `lblSandwich` | `Sandwich` |
| Button | `btnSandwich` | `$10.00` |
| Label | `lblPasta` | `Pasta` |
| Button | `btnPasta` | `$5.49` |
| Label | `lblSauce` | `Sauce` |
| Button | `btnSauce` | `$0.50` |
| Label | `lblWater` | `Water` |
| Button | `btnWater` | `$1.10` |
| ListBox | `lstReceipt` | leave empty |
| Button | `btnTotal` | `Total` |
| Label | `lblTotal` | `$0.00` |
| Button | `btnTotalTax` | `Total Tax / Switch` |

### Two overlapping practice-result panels

Place both Panels to the right of `btnTotalTax`, in the same position and at the same size. If one Panel covers the other while designing, use **Document Outline** or **Bring to Front / Send to Back** to select them.

| Control | `(Name)` | `Text` / setting |
|---|---|---|
| Panel | `pnlFivePercent` | `Visible: True` |
| Label inside 5% Panel | `lblFiveMode` | `5% mode` |
| Label inside 5% Panel | `lblFiveTax` | `$0.00` |
| Label inside 5% Panel | `lblFiveComplete` | `$0.00` |
| Panel | `pnlSevenPercent` | `Visible: False` |
| Label inside 7% Panel | `lblSevenMode` | `7% mode` |
| Label inside 7% Panel | `lblSevenTax` | `$0.00` |
| Label inside 7% Panel | `lblSevenComplete` | `$0.00` |

Use red text for the 5% panel and blue text for the 7% panel. The written `5% mode` / `7% mode` label is required; colour alone must not communicate the mode.

Run the Form before adding code. Confirm the 5% panel is visible, the 7% panel is hidden, and every other control is visible and aligned.

Suggested commit message: `Create practice concession register layout`

## Part 3 — Plan the fields before typing them

A field stores a value for the lifetime of the Form. Declaring a field does **not** make a calculation run continuously. The Click event is what runs the calculations.

At Form scope in `Form1.cs`, plan fields for these roles:

| Role | Suggested identifier | Type | Starting value |
|---|---|---|---|
| Running food total | `decTotal` | `decimal` | `0m` |
| 5% practice rate | `decFivePercentRate` | `decimal` | `0.05m` |
| 7% practice rate | `decSevenPercentRate` | `decimal` | `0.07m` |
| Tax calculated at 5% | `decFiveTax` | `decimal` | `0m` |
| Total plus 5% | `decFiveComplete` | `decimal` | `0m` |
| Tax calculated at 7% | `decSevenTax` | `decimal` | `0m` |
| Total plus 7% | `decSevenComplete` | `decimal` | `0m` |
| Which result is displayed | `bolShowSevenPercent` | `bool` | `false` |
| Whether a tax result has been displayed yet | `bolHasTaxResult` | `bool` | `false` |

Why two Boolean fields? The first tax click must show the default 5% result without switching immediately. After that first completed calculation, later clicks can flip the selected mode.

Before typing, point to the location in `Form1.cs` that is inside the `Form1` class but outside the constructor and every event handler. That is field scope.

Suggested commit message: `Add fields for both practice tax modes`

## Part 4 — Build the ordinary register behaviour

Work on one food button at a time.

For each food-button Click event:

1. add that item's decimal price to the running total field;
2. add a readable purchase line to `lstReceipt`;
3. run the Form and test that button twice;
4. confirm both the running total and receipt keep their earlier values.

Use a decimal literal for money. Remember that a decimal literal needs the `m` suffix. Keep the purchase wording consistent, for example: `Purchased: [item] for [price]`.

For `btnTotal`, display the current running total in `lblTotal` using the currency format string `C`.

Do not add tax in the food buttons or in `btnTotal`. Both practice tax calculations belong in the one `btnTotalTax` Click event.

Suggested commit message: `Add practice items receipt and running total`

## Part 5 — One Click event calculates both tax modes

Double-click `btnTotalTax` **once in the Designer** to generate its normal Click handler. That Designer double-click creates the handler; it is not a separate runtime DoubleClick feature.

Inside that one Click handler, work in this order:

1. Calculate the 5% tax from `decTotal` and the 5% rate field. Save it in the 5% tax field.
2. Add the running total and 5% tax. Save that result in the 5% complete-total field.
3. Calculate the 7% tax from the same `decTotal` and the 7% rate field. Save it in the 7% tax field.
4. Add the running total and 7% tax. Save that result in the 7% complete-total field.
5. Send both saved tax/complete-total pairs to their own labels using currency formatting.
6. On the first successful click, leave `bolShowSevenPercent` false so the 5% panel remains selected, then record that a result has now been displayed.
7. On every later click, reverse the Boolean mode with logical NOT: the new value is the opposite of the old value.
8. Make the 5% panel visible when `bolShowSevenPercent` is false.
9. Make the 7% panel visible when `bolShowSevenPercent` is true.

The visibility relationship you are trying to express is:

| `bolShowSevenPercent` | 5% Panel | 7% Panel |
|---|---|---|
| `false` | visible (`!false`) | hidden |
| `true` | hidden (`!true`) | visible |

This is where `!` belongs: it reverses a Boolean. It does not choose between `0.05m` and `0.07m`, and it does not perform either tax calculation.

### Why this uses Click, not DoubleClick

Use only the normal `Click` event at runtime. A physical double-click can raise Click activity as well as DoubleClick activity and can switch twice, making the visible result appear not to change. One Click handler is clearer: every press recalculates both results from the current total and then manages the display state.

Suggested commit message: `Calculate both tax modes and toggle visible result`

## Part 6 — Required tests

Write your predicted numbers before running each test. Use a calculator only after making the prediction.

| Test | Actions | Expected visible result |
|---|---|---|
| Default | Start the app | 5% panel visible; 7% panel hidden; all values `$0.00` |
| First tax click | Buy one Pizza, then click `Total Tax / Switch` | Both modes are calculated; 5% is displayed |
| Second tax click | Click the same button again without another purchase | Same totals; 7% is displayed |
| Third tax click | Click the same button again | Same totals; 5% is displayed again |
| Changed total | Buy one Water, then click the same button | Both modes recalculate from the new running total; display alternates once |
| Repeated item | Buy Coffee twice and click `Total` | Both purchases appear; ordinary total includes both |
| Currency | Test a value that produces more than two decimal places in tax | Visible money labels show currency formatting |

Use a breakpoint in the tax-button handler. In **Locals** or **Watch**, inspect the running total, both rates, both tax results, both complete totals, and both Boolean fields. Confirm the hidden values were calculated even though only one panel is visible.

## Completion checklist

- [ ] The repository and Form title both say **PRACTICE ONLY**.
- [ ] The Form follows the reference arrangement: food grid left, receipt right, totals below.
- [ ] All controls were created in the Designer before event code.
- [ ] Item buttons update one field-scoped running total and the receipt ListBox.
- [ ] `btnTotal` displays the running total with currency formatting.
- [ ] Both practice rate values are stored at Form scope.
- [ ] One normal Click handler calculates both 5% and 7% results.
- [ ] The first tax click displays 5%.
- [ ] Later clicks alternate 7%, 5%, 7% using logical NOT.
- [ ] Exactly one result panel is visible at a time.
- [ ] I can explain why fields store values but events run calculations.
- [ ] I can explain why `!` acts on a Boolean, not a decimal rate.
- [ ] I can explain every statement I wrote.
- [ ] My practice commits are pushed and visible on GitHub.

## Tutor boundary for the real A02

When returning to the real A02, do not copy this practice project, its fields, or its event plan. Start from Richard's real repository and follow his README. If you ask for help, the tutor may:

- ask what a control or variable should represent;
- explain a compiler/runtime error;
- ask you to predict a line's effect;
- point you to your class notes or the relevant concept;
- help you inspect Locals/Watch and interpret the value.

The tutor must not write, dictate, paste, or upload solution code for the real assignment.

