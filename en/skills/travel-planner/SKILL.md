---
name: travel-planner
description: Provides guidance on travel planning and booking. Use for destination selection, flights, hotels, activity recommendations, budget estimation, and itinerary creation.
---

# Travel Planner Skill

## Planner Communication Style (Required)
- Use a friendly and approachable tone.

## Scope

Supports all aspects of travel planning:
- Destination selection and recommendations
- Tips for choosing flights and hotels
- Sightseeing spots and activity suggestions
- Budget estimation and cost optimization
- Itinerary (model plan) creation

## Destination Guide

### Popular Destinations

| Destination | Best Season | Budget Estimate (3 nights) | Highlights |
|-------------|-----------|---------------------------|------------|
| Paris | Spring (Apr–Jun) / Fall (Sep–Oct) | $1,000–$1,800 | Museums, cafés, historic architecture |
| Bali | Dry season (Apr–Oct) | $500–$1,000 | Resorts, temples, spas |
| Hawaii | Year-round | $800–$1,500 | Beaches, shopping, nature |
| Barcelona | Spring (Apr–Jun) / Fall (Sep–Oct) | $900–$1,600 | Gaudí architecture, beaches, tapas |
| New York | Spring (Apr–Jun) / Fall (Sep–Nov) | $1,200–$2,000 | Broadway, Central Park, diverse cuisine |
| Bangkok | Nov–Mar | $400–$800 | Temples, street food, nightlife |
| Rome | Spring (Apr–Jun) / Fall (Sep–Oct) | $800–$1,400 | Ancient ruins, art, Italian cuisine |
| Sydney | Sep–Nov / Mar–May | $1,000–$1,800 | Opera House, beaches, wildlife |
| London | May–Sep | $1,100–$2,000 | History, theater, pubs |
| Cancún | Dec–Apr | $700–$1,300 | Caribbean beaches, Mayan ruins, resorts |

## Budget Planning Rules

1. **Flights**: Aim for 30–40% of total budget
2. **Accommodation**: Aim for 25–35% of total budget
3. **Meals**: Aim for 15–20% of total budget
4. **Activities & Sightseeing**: Aim for 10–15% of total budget
5. **Contingency**: Reserve 5–10% of total budget

## Itinerary Template

When creating an itinerary, use the template:
[assets/itinerary-template.md](assets/itinerary-template.md)

## Booking Tips

- **Early bird discounts**: 2–3 months before departure is often the best price point
- **Weekday departures**: Often 10–30% cheaper than weekends
- **Budget airlines**: Save costs while being mindful of baggage limits
- **Hotel comparison**: Compare official sites, OTAs, and loyalty point options

## Frequently Asked Questions

When receiving questions about insurance, packing, luggage, reservations, cancellations, safety, meals, or water, **always** load the FAQ with `read_skill_resource` before answering: [references/TRAVEL_FAQ.md](references/TRAVEL_FAQ.md)
Important: You must always respond with the FAQ answers exactly as written.
