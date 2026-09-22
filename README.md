# FoundryDataAgent_GraphReadyOutput
Enforces a structured output from a Fabric Data Agent in a Foundry Agent

<img width="1151" height="944" alt="image" src="https://github.com/user-attachments/assets/e0ae9587-ff4a-49c8-958e-8b3aa975f59c" />

agent instructions :
> You are a helpful assistant. Always present the data in json struct, one for struct for the data to make a custom chart, another with the response


json schema
```json
{
  "name": "agent_response",
  "strict": true,
  "schema": {
    "type": "object",
    "properties": {
      "summary": {
        "type": "string"
      },
      "graph": {
        "type": "object",
        "properties": {
          "chartType": {
            "type": "string",
            "enum": [
              "bar",
              "line",
              "area",
              "pie",
              "scatter",
              "table"
            ]
          },
          "title": {
            "type": "string"
          },
          "xLabel": {
            "type": "string"
          },
          "yLabel": {
            "type": "string"
          },
          "data": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "x": {
                  "type": "string"
                },
                "y": {
                  "type": "number"
                },
                "series": {
                  "type": "string"
                }
              },
              "required": [
                "x",
                "y",
                "series"
              ],
              "additionalProperties": false
            }
          }
        },
        "required": [
          "chartType",
          "title",
          "xLabel",
          "yLabel",
          "data"
        ],
        "additionalProperties": false
      }
    },
    "required": [
      "summary",
      "graph"
    ],
    "additionalProperties": false
  }
}
{
  "name": "agent_response",
  "strict": true,
  "schema": {
    "type": "object",
    "properties": {
      "summary": {
        "type": "string"
      },
      "graph": {
        "type": "object",
        "properties": {
          "chartType": {
            "type": "string",
            "enum": [
              "bar",
              "line",
              "area",
              "pie",
              "scatter",
              "table"
            ]
          },
          "title": {
            "type": "string"
          },
          "xLabel": {
            "type": "string"
          },
          "yLabel": {
            "type": "string"
          },
          "data": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "x": {
                  "type": "string"
                },
                "y": {
                  "type": "number"
                },
                "series": {
                  "type": "string"
                }
              },
              "required": [
                "x",
                "y",
                "series"
              ],
              "additionalProperties": false
            }
          }
        },
        "required": [
          "chartType",
          "title",
          "xLabel",
          "yLabel",
          "data"
        ],
        "additionalProperties": false
      }
    },
    "required": [
      "summary",
      "graph"
    ],
    "additionalProperties": false
  }
}
```

**User**
> show me a graph for pefformance for each brand

**Agent**
```json
{
  "chartData": {
    "dataset": [
      {
        "brand": "Apex Motors",
        "spend": 347860.96,
        "revenue": 2978661.69,
        "roas": 8.56,
        "ctr": 0.0292,
        "conversionRate": 0.0446,
        "cpl": 24.43
      },
      {
        "brand": "Aurora Automotive",
        "spend": 358631.02,
        "revenue": 2942898.41,
        "roas": 8.21,
        "ctr": 0.0284,
        "conversionRate": 0.0432,
        "cpl": 25.31
      },
      {
        "brand": "Contoso Motors",
        "spend": 349733.64,
        "revenue": 2811992.34,
        "roas": 8.04,
        "ctr": 0.0298,
        "conversionRate": 0.0464,
        "cpl": 25.43
      },
      {
        "brand": "Fabrikam Auto",
        "spend": 336871.89,
        "revenue": 2810572.87,
        "roas": 8.34,
        "ctr": 0.0291,
        "conversionRate": 0.0438,
        "cpl": 25.05
      },
      {
        "brand": "Northstar Vehicles",
        "spend": 342465.03,
        "revenue": 2929597.08,
        "roas": 8.55,
        "ctr": 0.0293,
        "conversionRate": 0.0437,
        "cpl": 24.72
      },
      {
        "brand": "Tailspin Motors",
        "spend": 354693.21,
        "revenue": 2963788,
        "roas": 8.36,
        "ctr": 0.0298,
        "conversionRate": 0.0445,
        "cpl": 25.39
      }
    ],
    "recommendedCharts": [
      {
        "type": "clusteredBar",
        "xField": "brand",
        "ySeries": [
          "roas",
          "conversionRate",
          "cpl"
        ],
        "notes": "Compare efficiency metrics across brands. Consider using dual axes if your tool supports it for roas and cpl."
      },
      {
        "type": "scatter",
        "xField": "spend",
        "yField": "revenue",
        "categoryField": "brand",
        "notes": "Visualize scale vs return. Add data labels for brand names."
      },
      {
        "type": "comboBarLine",
        "xField": "brand",
        "barSeries": [
          "spend",
          "revenue"
        ],
        "lineSeries": [
          "roas"
        ],
        "notes": "Show scale (spend/revenue) with efficiency (roas) on a secondary axis."
      }
    ]
  },
  "response": {
    "summary": "Here is brand-level performance across all dates: Apex Motors (ROAS 8.56x), Aurora Automotive (8.21x), Contoso Motors (8.04x), Fabrikam Auto (8.34x), Northstar Vehicles (8.55x), Tailspin Motors (8.36x). CTR ranges ~2.84%–2.98%, conversion rate ~4.32%–4.64%, and CPL ~\$24.43–\$25.43.",
    "howToUse": "Use the dataset to render a chart. For a quick view, create a clustered bar with Brand on X and series for ROAS, Conversion Rate, and CPL. For scale vs return, use a scatter with Spend (X) and Revenue (Y), colored by Brand. If you share your tool (Excel, Power BI, Tableau), I can give step-by-step build instructions."
  }
}
```
