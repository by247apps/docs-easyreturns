# Benachrichtigungen

-   [Händler Benachrichtigungen](#merchant)
-   [Kunden Benachrichtigungen](#customer)
-   [FAQ](#faq)

<a name="merchant"></a>

## Händler Benachrichtigungen

Shopify versendet für jede Retourenanfrage eine Benachrichtigung an die Haupt-Email-Adresse deines Shopify Stores. Über easyReturns kannst du diese Art der Benachrichtigung an eine alternative E-Mail Adresse senden lassen. Diese E-Mail beinhaltet einen Link zur Ansicht der Retoure in easyReturns.

Zusätzlich kann easyReturns weiter Benachrichtigungen versenden und zwar

-   Wenn Retoure vom Kunden storniert wurde
-   Wenn die Erstellung des Retoure-Labels fehlschlug

<a name="customer"></a>

## Kunden Benachrichtigungen

Die Benachrichtigungen die von Shopify versendet werden können über die Shopify Liquid Templates angepasst werden. Wir verlinken in der App zu den entprechenden templates. Jede von Shopify versendete Nachricht wird im Verlauf einer jeden Bestellung angezeigt. <a class="video">https://youtu.be/V8O8bFzL7U4</a>

Wir empfehlen das folgende Snippet für die - _Rückgabe genehmigt_ - Benachrichtigung zu verwenden. Über das Icon oben rechts kannst du dieses in die Zwischenablage kopieren und den bisherigen Liquid code mit copy 6 paste ersetzen.

```HTML
<!DOCTYPE html>
<html lang="de">
<head>
  <title>{{ email_title }}</title>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <meta name="viewport" content="width=device-width">
  <link rel="stylesheet" type="text/css" href="/assets/notifications/styles.css">
  <style>
    .button__cell { background: {{ shop.email_accent_color }}; }
    a, a:hover, a:active, a:visited { color: {{ shop.email_accent_color }}; }
  </style>
</head>

<body>
  <table class="body">
    <tr>
      <td>
        <table class="header row">
  <tr>
    <td class="header__cell">
      <center>

        <table class="container">
          <tr>
            <td>

              <table class="row">
                <tr>
                  <td class="shop-name__cell">
                    {%- if shop.email_logo_url %}
                      <img src="{{shop.email_logo_url}}" alt="{{ shop.name }}" width="{{ shop.email_logo_width }}">
                    {%- else %}
                      <h1 class="shop-name__text">
                        <a href="{{shop.url}}">{{ shop.name }}</a>
                      </h1>
                    {%- endif %}
                  </td>

                    <td>
                      <table class="order-po-number__container">
                        <tr>
                          <td class="order-number__cell">
                            <span class="order-number__text">
                              Bestellung {{ order.name }}
                            </span>
                          </td>
                        </tr>
                        {%- if po_number %}
                            <tr>
                              <td class="po-number__cell">
                                <span class="po-number__text">
                                  Bestellnummer {{ po_number }}
                                </span>
                              </td>
                            </tr>
                        {%- endif %}
                      </table>
                    </td>
                </tr>
              </table>

            </td>
          </tr>
        </table>

      </center>
    </td>
  </tr>
</table>


        <table class="row content">
  <tr>
    <td class="content__cell">
      <center>
        <table class="container">
          <tr>
            <td>

          {% for return_delivery in return.deliveries %}
            {% if return_delivery.type == 'shopify_label' %}
              <h2>Die Dokumente für deine Rücksendung sind fertig</h2>
              <p class="return-creation__subtitle">Rufe die Dokumente auf und folge den Anweisungen.</p>

              {% capture url_primary %}{{ return_delivery.return_label.public_file_url }}{% endcapture %}
              {% capture text_primary %}Dokumente aufrufen{% endcapture %}
              {% capture url_secondary %}{{ return.checkout_payment_collection_url }}{% endcapture %}
              {% capture text_secondary %}Jetzt bezahlen{% endcapture %}

              <table class="row actions">
                <tr>
                  <td class="empty-line">&nbsp;</td>
                </tr>
                <tr>
                  <td class="actions__cell">
                    {% if url_primary != blank or url_secondary != blank %}
                      {% if url_primary != blank %}
                    <table class="button main-action-cell">
                      <tr>
                        <td class="button__cell">
                          <a href="{{ url_primary }}" class="button__text">{{ text_primary }}</a>
                        </td>
                      </tr>
                    </table>
                      {% endif %}
                      {% if url_secondary != blank %}
                    <table class="button return__mobile-padding main-action-cell">
                      <tr>
                        <td class="button__cell">
                          <a href="{{ url_secondary }}" class="button__text return__main-button">{{ text_secondary }}</a>
                        </td>
                      </tr>
                    </table>
                      {% endif %}
                    <table class="link secondary-action-cell">
                      <tr>
                        <td class="link__cell">oder <a target="_blank" href="{{ order.order_status_url }}">Deine Bestellung ansehen</a></td>
                      </tr>
                    </table>
                    {% else %}
                    <table class="button main-action-cell">
                      <tr>
                        <td class="button__cell"><a href="{{ order.order_status_url }}" class="button__text">Deine Bestellung ansehen</a></td>
                      </tr>
                    </table>
                    {% endif %}
                  </td>
                </tr>
              </table>

            {% endif %}
          {% endfor %}

            </td>
          </tr>
        </table>
      </center>
    </td>
  </tr>
</table>

        {% if return.line_items.size > 0 %}
          <table class="row content">
  <tr>
    <td class="content__cell">
      <center>
        <table class="container">
          <tr>
            <td>

            <h2>Zurückzugebende Artikel</h2>

<table class="row">
  {% for line_item in return.line_items %}
  <tr class="order-list__item">
    <td class="order-list__item__cell">
      <table>
        <td>
          {% if line_item.image %}
            <img src="{{ line_item | img_url: 'compact_cropped' }}" align="left" width="60" height="60" class="order-list__product-image"/>
          {% endif %}
        </td>
        <td class="order-list__product-description-cell">
          {% assign line_display = line_item.quantity  %}

          <span class="order-list__item-title">{{ line_item.title_without_variant }}&nbsp;&times;&nbsp;{{ line_display }}</span><br/>

          {% if line_item.variant.title != 'Default Title' %}
            <span class="order-list__item-variant">{{ line_item.variant.title }}</span><br/>
          {% endif %}

          {% if line_item.discount_allocations %}
            {% for discount_allocation in line_item.discount_allocations %}
              {% if discount_allocation.amount > 0 %}
              <p>
                <span class="order-list__item-discount-allocation">
                  <img src="{{ 'notifications/discounttag.png' | shopify_asset_url }}" width="18" height="18" class="discount-tag-icon" />
                  <span>
                    {{ discount_allocation.discount_application.title | upcase }}
                    (-{{ discount_allocation.amount | money }})
                  </span>
                </span>
              </p>
              {% endif %}
            {% endfor %}
          {% endif %}
        </td>

        <td class="order-list__price-cell">
          {% if line_item.original_line_price != line_item.final_line_price %}
            <del class="order-list__item-original-price">{{ line_item.original_line_price | money }}</del>
          {% endif %}
          <p class="order-list__item-price">
            {% if line_item.final_line_price > 0 %}
              {% capture final_line_price %}
                  -{{ line_item.final_line_price | money }}
              {% endcapture %}
              {{ final_line_price }}
                {% if line_item.unit_price_measurement %}
                  <div class="order-list__unit-price">
                    {{ line_item.unit_price | money }}/
                    {%- if line_item.unit_price_measurement.reference_value != 1 -%}
                      {{- line_item.unit_price_measurement.reference_value -}}
                    {%- endif -%}
                    {{ line_item.unit_price_measurement.reference_unit }}
                  </div>
                {% endif %}
            {% else %}
              Kostenlos
            {% endif %}
          </p>
        </td>
      </table>
    </td>
  </tr>
  {% endfor %}
</table>


            </td>
          </tr>
        </table>
      </center>
    </td>
  </tr>
</table>
        {% endif %}

        {% if return.exchange_line_items.size > 0 %}
          <table class="row content">
  <tr>
    <td class="content__cell">
      <center>
        <table class="container">
          <tr>
            <td>

            <h2>Artikel, die du erhältst</h2>

<table class="row">
  {% for line_item in return.exchange_line_items %}
  <tr class="order-list__item">
    <td class="order-list__item__cell">
      <table>
        <td>
          {% if line_item.image %}
            <img src="{{ line_item | img_url: 'compact_cropped' }}" align="left" width="60" height="60" class="order-list__product-image"/>
          {% endif %}
        </td>
        <td class="order-list__product-description-cell">
          {% assign line_display = line_item.quantity  %}

          <span class="order-list__item-title">{{ line_item.title_without_variant }}&nbsp;&times;&nbsp;{{ line_display }}</span><br/>

          {% if line_item.variant.title != 'Default Title' %}
            <span class="order-list__item-variant">{{ line_item.variant.title }}</span><br/>
          {% endif %}

          {% if line_item.discount_allocations %}
            {% for discount_allocation in line_item.discount_allocations %}
              {% if discount_allocation.amount > 0 %}
              <p>
                <span class="order-list__item-discount-allocation">
                  <img src="{{ 'notifications/discounttag.png' | shopify_asset_url }}" width="18" height="18" class="discount-tag-icon" />
                  <span>
                    {{ discount_allocation.discount_application.title | upcase }}
                    (-{{ discount_allocation.amount | money }})
                  </span>
                </span>
              </p>
              {% endif %}
            {% endfor %}
          {% endif %}
        </td>

        <td class="order-list__price-cell">
          {% if line_item.original_line_price != line_item.final_line_price %}
            <del class="order-list__item-original-price">{{ line_item.original_line_price | money }}</del>
          {% endif %}
          <p class="order-list__item-price">
            {% if line_item.final_line_price > 0 %}
              {% capture final_line_price %}
                  {{ line_item.final_line_price | money }}
              {% endcapture %}
              {{ final_line_price }}
                {% if line_item.unit_price_measurement %}
                  <div class="order-list__unit-price">
                    {{ line_item.unit_price | money }}/
                    {%- if line_item.unit_price_measurement.reference_value != 1 -%}
                      {{- line_item.unit_price_measurement.reference_value -}}
                    {%- endif -%}
                    {{ line_item.unit_price_measurement.reference_unit }}
                  </div>
                {% endif %}
            {% else %}
              Kostenlos
            {% endif %}
          </p>
        </td>
      </table>
    </td>
  </tr>
  {% endfor %}
</table>


            </td>
          </tr>
        </table>
      </center>
    </td>
  </tr>
</table>
        {% endif %}

        <table class="row content">
  <tr>
    <td class="content__cell">
      <center>
        <table class="container">
          <tr>
            <td>

          <table class="row subtotal-lines">
  <tr>
    <td class="subtotal-spacer"></td>
    <td>
      <table class="row subtotal-table">

        {% capture line_items_subtotal_price %}
          {% if return.line_items_subtotal_price < 0 %}
            -{{ return.line_items_subtotal_price  | abs | money }}
          {% else %}
            {{ return.line_items_subtotal_price | money }}
          {% endif %}
        {% endcapture %}


<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>Zwischensumme</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ line_items_subtotal_price }}</strong>
  </td>
</tr>


        {% assign fees = return.fees %}
        {% for fee in fees %}

<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>{{ fee.title }}</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ fee.subtotal | money }}</strong>
  </td>
</tr>

{% endfor %}


        {% if return.total_tax_price %}
          {% capture total_tax_price %}
            {% if return.total_tax_price < 0 %}
              -{{ return.total_tax_price | abs | money }}
            {% else %}
              {{ return.total_tax_price | money }}
            {% endif %}
          {% endcapture %}

<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>Geschätzte Steuern</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ total_tax_price }}</strong>
  </td>
</tr>

        {% endif %}

        {%  if return.pre_return_order_total_outstanding && return.pre_return_order_total_outstanding != 0 %}

<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>Ausstehender Betrag</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ return.pre_return_order_total_outstanding | money_with_currency }}</strong>
  </td>
</tr>

        {% endif %}

        {% if return.order_total_outstanding > 0 %}
        <table class="row subtotal-table subtotal-table--total">

<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>Zu zahlender Betrag</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ return.order_total_outstanding | money_with_currency }}</strong>
  </td>
</tr>

        </table>
        {% elsif return.order_total_outstanding <= 0 %}
        <table class="row subtotal-table subtotal-table--total">

<tr class="subtotal-line">
  <td class="subtotal-line__title">
    <p>
      <span>Geschätzte Rückerstattung</span>
    </p>
  </td>
  <td class="subtotal-line__value">
      <strong>{{ return.order_total_outstanding | abs | money_with_currency }}</strong>
  </td>
</tr>

        </table>
        {% endif %}
      </table>
    </td>
  </tr>
</table>


            </td>
          </tr>
        </table>
      </center>
    </td>
  </tr>
</table>

        <table class="row footer">
  <tr>
    <td class="footer__cell">
      <center>
        <table class="container">
          <tr>
            <td>

              <p class="disclaimer__subtext">Falls du Fragen hast, antworte auf diese E-Mail oder kontaktiere uns unter <a href="mailto:{{ shop.email }}">{{ shop.email }}</a>.</p>
            </td>
          </tr>
        </table>
      </center>
    </td>
  </tr>
</table>

<img src="{{ 'notifications/spacer.png' | shopify_asset_url }}" class="spacer" height="1" />

      </td>
    </tr>
  </table>
</body>
</html>
```

<a name="faq"></a>

## FAQ

<div class="faq-list">
<dl class="space-y-8">
<div>
<dt><h4></h4></dt>
<dd>
</dd>
</div>
</dl>

</div>
