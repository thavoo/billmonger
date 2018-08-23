Billmonger
==========

Billmonger is a dead simple PDF one-page invoice generator written in Go. The
intention is to make the generated invoices look professional and have them be
repeatable. You can use your own company logo and two company colors as part of
the invoice, and each invoice is configurable with a single YAML file.

Billmonger makes many assumptions to keep things simple. Some of them
are:

 * You will have two company colors or use two generic colors
 * You will not invoice for more than about a dozen items
 * The billing period is a month (semi-configurable)
 * The bill due date is a month boundary
 * Everything on the bill is the same currency
 * Filenames will be output in a standard way

Current limitations:
 * It almost has support for tax calculation but it's not there yet

The Problem This Solves
------------------------

You have a small business and need to regularly generate bills, perhaps as a
contractor. Your bills are fairly similar but may have different line items.
This will generate a nice A4 PDF that looks professional and is easily
customizable to your business.

What It Looks Like
------------------

The sample `billing.example.yaml` file [provided](billing.example.yaml) will
generate a [PDF file](assets/example.pdf) that looks like this:

![PDF Example](assets/example.png)

Configuration
-------------

Configuration is done in the `billing.yaml` file. Currently that's hardcoded,
but will be CLI switchable soon. This describes the bill and the billables to
be reported. It supports a couple of templating features that make reporting
items easier. These are Go template functions and are to be put inside double
curly braces anywhere in the YAML file. Interpretation of the template happens
_before_ YAML processing. Examples:

 * `{{ endOfNexMonth }}`: This will be substituted with the end day of the
   month following the current month.
 * `{{ billingPeriod }}`: This will be substituted with the current month's
   beginning and end dates.