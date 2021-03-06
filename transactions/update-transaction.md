---
description: >-
  Use this endpoint to update a single transaction. You may also use this to
  split an existing transaction.
---

# Update transaction

{% api-method method="put" host="https://dev.lunchmoney.app" path="/v1/transactions/:transaction\_id" %}
{% api-method-summary %}
Update transaction
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="split" type="object" required=false %}
Defines the split of a transaction. You may not split an already-split transaction, recurring transaction, or group transaction.  
See Split object for supported properties.
{% endapi-method-parameter %}

{% api-method-parameter name="transaction" type="object" required=true %}
Updates to transaction matching ID \(see Update Transaction object below\)
{% endapi-method-parameter %}

{% api-method-parameter name="debit\_as\_negative" type="boolean" required=false %}
If true, will assume negative amount values denote expenses and positive amount values denote credits. Defaults to false.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
If a split was part of the request, an array of newly-created split transactions will be returned.
{% endapi-method-response-example-description %}

```text
{
    updated: true,
    split: [58, 59]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Array of errors will be returned if field\(s\) are invalid.
{% endapi-method-response-example-description %}

```text
{ error:
   [ 'This transaction doesn't exist or you don't have access to it.' ] }

{ error:
   [ 'You cannot change the amount for this transaction because it was automatically imported.',
     'You cannot assign an asset_id for this transaction because it was automatically imported.' ] }
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="Update Transaction object" %}
### Update Transaction object

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left"></th>
      <th style="text-align:center">Type</th>
      <th style="text-align:left"></th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>date</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Must be in ISO 8601 format (YYYY-MM-DD).</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category_id</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Unique identifier for associated category_id. Category must be associated
        with the same account and must not be a category group.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>payee</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Max 140 characters</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>amount</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number | string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">You may only update this if this transaction was not created from an automatic
        import, i.e. if this transaction is not associated with a plaid_account_id</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>currency</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">You may only update this if this transaction was not created from an automatic
        import, i.e. if this transaction is not associated with a plaid_account_id.
        Defaults to user account&apos;s primary currency.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>asset_id</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Unique identifier for associated asset (manually-managed account). Asset
        must be associated with the same account. You may only update this if this
        transaction was not created from an automatic import, i.e. if this transaction
        is not associated with a plaid_account_id</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>recurring_id</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Unique identifier for associated recurring expense. Recurring expense
        must be associated with the same account.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>notes</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Max 350 characters</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>status</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Must be either <code>cleared</code> or <code>uncleared</code>. Defaults to <code>uncleared</code>
        <br
        />If recurring_id is provided, the status will automatically be set to <code>recurring</code> or <code>recurring_suggested</code> depending
        on the type of recurring_id. Defaults to <code>uncleared</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>external_id</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">User-defined external ID for transaction. Max 75 characters. External
        IDs must be unique within the same asset_id. You may only update this if
        this transaction was not created from an automatic import, i.e. if this
        transaction is not associated with a plaid_account_id</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">array of numbers and/or strings</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Passing in a number will attempt to match by ID. If no matching tag ID
          is found, an error will be thrown.</p>
        <p>Passing in a string will attempt to match by string. If no matching tag
          name is found, a new tag will be created.</p>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Split object" %}
### Split object

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left"></th>
      <th style="text-align:center">Type</th>
      <th style="text-align:left"></th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>date</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Must be in ISO 8601 format (YYYY-MM-DD)</p>
        <p><em>Required.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category_id</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Unique identifier for associated category_id. Category must be associated
          with the same account.</p>
        <p><em>Required.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>notes</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>amount</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:center">number | string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Individual amount of split. Currency will inherit from parent transaction.
          All amounts must sum up to parent transaction amount.</p>
        <p><em>Required.</em>
        </p>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

