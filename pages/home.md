---
name: Home
assetId: 822a741e-e1da-45c0-a2dd-25c7a1cda514
type: page
---

# Sales Dashboard

{% dropdown
    id="category_filter"
    data="demo_daily_orders"
    value_column="category"
    title="Category"
/%}

{% big_value
    data="demo_daily_orders"
    value="sum(total_sales)"
    fmt="usd1m"
    title="Total Revenue"
    filters=["category_filter"]
    date_range={
        date="date"
        range="last 12 months"
    }
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="sum(transactions)"
    fmt="#,##0"
    title="Total Orders"
    filters=["category_filter"]
    date_range={
        date="date"
        range="last 12 months"
    }
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="avg(avg_transaction_value)"
    fmt="usd2"
    title="Avg Order Value"
    filters=["category_filter"]
    date_range={
        date="date"
        range="last 12 months"
    }
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="line"
        x="date"
        date_grain="month"
    }
/%}

## Revenue Over Time

{% line_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    y_fmt="usd0m"
    series="category"
    date_grain="month"
    title="Monthly Revenue by Category"
    filters=["category_filter"]
/%}

## Sales by Category

{% bar_chart
    data="demo_daily_orders"
    x="category"
    y="sum(total_sales)"
    y_fmt="usd0m"
    title="Total Revenue by Category"
    order="sum(total_sales) desc"
    filters=["category_filter"]
/%}

## Sales Channel Mix

{% bar_chart
    data="demo_order_details"
    x="date"
    y="sum(quantity)"
    series="category"
    stacked="100%"
    date_grain="month"
    title="Category Mix Over Time"
/%}

## Seasonality

{% bar_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    y_fmt="usd"
    date_grain="month of year"
    title="Revenue by Month of Year"
    subtitle="Identify seasonal patterns"
    filters=["category_filter"]
/%}

## Performance Summary

{% table
    data="demo_daily_orders"
    filters=["category_filter"]
    title="Revenue by Category & Year"
%}
    {% dimension
        value="category"
    /%}
    {% pivot
        value="date"
        date_grain="year"
    /%}
    {% measure
        value="sum(total_sales)"
        fmt="usd0m"
    /%}
{% /table %}
