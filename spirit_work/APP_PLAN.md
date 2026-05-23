# Tarot Card Reading Journal & Tracking App
## Development Plan

### Technology Stack
- **Backend:** Flask (Python web framework)
- **Storage:** Text file (JSON format for easy parsing)
- **Frontend:** HTML/CSS/JavaScript (vanilla, or minimal framework)

---

## Project Structure

```
spirit_work/
├── app.py                 # Main Flask application
├── readings.txt           # Text file storing all readings (JSON format)
├── tarot_cards.json       # All tarot card names for autocomplete
├── templates/
│   ├── index.html        # Main input page
│   └── readings.html     # View/display page (future)
├── static/
│   ├── css/
│   │   └── style.css     # Styling
│   └── js/
│       └── script.js     # JavaScript for toggling spreads & autocomplete
└── requirements.txt       # Python dependencies
```

---

## Features

### Phase 1: Basic Input (Current Focus)

#### 1. Card Input Page (`index.html`)
- **Toggle Switch/Button:** 
  - Switch between "1 Card Spread" and "3 Card Spread"
  - JavaScript handles showing/hiding card input fields dynamically

- **Card Input Fields:**
  - **For 1 Card Spread:**
    - Card Name input (text field with **autocomplete**)
    - Checkbox: "Reversed" (checked = reversed, unchecked = upright)
  
  - **For 3 Card Spread:**
    - Card 1: Name input (with **autocomplete**) + Reversed checkbox
    - Card 2: Name input (with **autocomplete**) + Reversed checkbox  
    - Card 3: Name input (with **autocomplete**) + Reversed checkbox
    - (Optional: Position labels - Theme/Lesson/Focus, or Past/Present/Future)
  
  - **Autocomplete Feature:**
    - Card name inputs use HTML5 `<datalist>` or custom JavaScript autocomplete
    - Suggestions loaded from `tarot_cards.json`
    - Filters cards as user types (case-insensitive)
    - Shows matching card names in dropdown

- **Additional Fields:**
  - Date (auto-populate with today's date, but editable)
  - Question/Intention (optional text area)
  - Notes/Reflection (optional text area)

- **Submit Button:**
  - Saves reading to `readings.txt`
  - Redirects to success message or back to input page

---

## Data Storage Format

### Text File: `readings.txt`
Store each reading as a JSON object, one per line (JSONL format):

```json
{"id": 1, "date": "2025-01-15", "spread_type": "3", "cards": [{"name": "3 of Pentacles", "reversed": true}, {"name": "3 of Swords", "reversed": false}, {"name": "3 of Wands", "reversed": false}], "question": "What does the universe want me to know today?", "notes": ""}
{"id": 2, "date": "2025-01-16", "spread_type": "1", "cards": [{"name": "The Moon", "reversed": false}], "question": "Daily guidance", "notes": "Felt very intuitive"}
```

**Data Structure:**
- `id`: Unique identifier (auto-increment)
- `date`: Date string (YYYY-MM-DD format)
- `spread_type`: "1" or "3"
- `cards`: Array of card objects
  - `name`: Card name (string)
  - `reversed`: Boolean (true = reversed, false = upright)
- `question`: Optional string
- `notes`: Optional string

---

## Flask Application Structure

### `app.py` - Main Routes

1. **GET `/`** 
   - Renders `index.html` input form
   - Passes current spread type preference to template

2. **POST `/submit`**
   - Receives form data
   - Validates input
   - Appends new reading to `readings.txt` (JSON format)
   - Generates unique ID (read last ID from file, increment)
   - Returns success message or redirects

3. **GET `/api/cards`**
   - Reads `tarot_cards.json`
   - Returns JSON array of all card names
   - Used for autocomplete functionality

4. **GET `/readings`** (Future)
   - Reads all readings from `readings.txt`
   - Parses JSON lines
   - Displays list of readings

---

## Frontend: Input Form Logic

### JavaScript Functions Needed

1. **`toggleSpreadType(spreadType)`**
   - Shows/hides card input fields based on selection
   - If "1 Card": show 1 card input group
   - If "3 Card": show 3 card input groups
   - Clears any previously entered card data when switching

2. **`loadCardNames()`**
   - Fetch card names from `/api/cards` endpoint on page load
   - Store in JavaScript array for autocomplete
   - Initialize autocomplete on all card name input fields

3. **`setupAutocomplete(inputElement, cardNames)`**
   - Set up autocomplete/datalist for a given input field
   - Filter card names as user types
   - Handle case-insensitive matching
   - Use HTML5 `<datalist>` or custom dropdown

4. **Form Validation**
   - Ensure at least card name(s) are filled
   - Validate date format if manually entered
   - Optionally validate card names against known cards list

5. **Submit Handler**
   - Collect form data
   - Format as JSON
   - POST to `/submit` endpoint

---

## Implementation Steps

### Step 1: Setup Flask Project
1. Create `requirements.txt` with Flask dependency
2. Create basic `app.py` with Flask app instance
3. Create `templates/` and `static/` directories

### Step 2: Create Input Form (`index.html`)
1. Build HTML form structure
2. Add toggle switch/buttons for spread type
3. Create card input fields (initially hidden for 3-card)
4. Add date, question, notes fields
5. Add submit button

### Step 3: Add JavaScript Functionality
1. Implement `toggleSpreadType()` function
2. Show/hide card inputs based on selection
3. Implement `loadCardNames()` to fetch from `/api/cards`
4. Implement `setupAutocomplete()` for each card input field
5. Handle form submission

### Step 4: Backend Logic (`app.py`)
1. Create route handlers (GET `/`, POST `/submit`, GET `/api/cards`)
2. Implement file reading/writing functions:
   - `read_readings()` - Read all readings from file
   - `write_reading(reading_data)` - Append new reading
   - `get_next_id()` - Generate next ID
   - `load_card_names()` - Read `tarot_cards.json` and return card list
3. Handle form data parsing and validation

### Step 5: Styling (`style.css`)
1. Basic layout and styling
2. Responsive design considerations
3. Form styling (inputs, checkboxes, buttons)

### Step 6: Testing
1. Test 1-card spread input
2. Test 3-card spread input
3. Test toggle between spreads
4. Verify data saves correctly to file
5. Verify JSON format is correct

---

## File Reading/Writing Functions

### Python Helper Functions (in `app.py`)

**Loading Card Names:**

```python
import json
import os

CARDS_FILE = 'tarot_cards.json'

def load_card_names():
    """Load all card names from tarot_cards.json"""
    if os.path.exists(CARDS_FILE):
        with open(CARDS_FILE, 'r') as f:
            data = json.load(f)
            return data.get('all_cards', [])
    return []
```

**Card Names API Route:**

```python
@app.route('/api/cards')
def api_cards():
    """Return JSON array of all card names for autocomplete"""
    cards = load_card_names()
    return jsonify(cards)
```

### Reading/Writing Functions

```python
import json
import os
from datetime import datetime

READINGS_FILE = 'readings.txt'

def read_readings():
    """Read all readings from text file, return list of dicts"""
    readings = []
    if os.path.exists(READINGS_FILE):
        with open(READINGS_FILE, 'r') as f:
            for line in f:
                if line.strip():
                    readings.append(json.loads(line))
    return readings

def write_reading(reading_data):
    """Append a new reading to the file"""
    with open(READINGS_FILE, 'a') as f:
        f.write(json.dumps(reading_data) + '\n')

def get_next_id():
    """Get the next available ID by reading existing readings"""
    readings = read_readings()
    if not readings:
        return 1
    return max(r['id'] for r in readings) + 1
```

---

## HTML Form Structure

### Input Fields (1 Card Spread)
```html
<div id="card-1-input" class="card-input-group">
    <label>Card Name:</label>
    <input type="text" name="card_1_name" id="card_1_name" list="card-suggestions" required>
    <datalist id="card-suggestions">
        <!-- Options populated by JavaScript -->
    </datalist>
    <label>
        <input type="checkbox" name="card_1_reversed" value="true">
        Reversed
    </label>
</div>
```

**Note:** Alternatively, you can use a custom JavaScript autocomplete library or build a simple one that filters and displays matching cards as the user types.

### Input Fields (3 Card Spread)
```html
<div id="card-3-inputs" class="card-input-group">
    <div class="card-input">
        <label>Card 1 Name:</label>
        <input type="text" name="card_1_name" id="card_1_name" list="card-suggestions" required>
        <label>
            <input type="checkbox" name="card_1_reversed" value="true">
            Reversed
        </label>
    </div>
    <div class="card-input">
        <label>Card 2 Name:</label>
        <input type="text" name="card_2_name" id="card_2_name" list="card-suggestions" required>
        <label>
            <input type="checkbox" name="card_2_reversed" value="true">
            Reversed
        </label>
    </div>
    <div class="card-input">
        <label>Card 3 Name:</label>
        <input type="text" name="card_3_name" id="card_3_name" list="card-suggestions" required>
        <label>
            <input type="checkbox" name="card_3_reversed" value="true">
            Reversed
        </label>
    </div>
</div>
```

**JavaScript Autocomplete Example:**

```javascript
// Load card names on page load
let allCards = [];

async function loadCardNames() {
    try {
        const response = await fetch('/api/cards');
        allCards = await response.json();
        setupAutocomplete();
    } catch (error) {
        console.error('Error loading card names:', error);
    }
}

function setupAutocomplete() {
    // Get all card input fields
    const cardInputs = document.querySelectorAll('input[name*="card"][name*="name"]');
    
    // Populate datalist
    const datalist = document.getElementById('card-suggestions');
    allCards.forEach(card => {
        const option = document.createElement('option');
        option.value = card;
        datalist.appendChild(option);
    });
    
    // Optional: Add custom filtering for better UX
    cardInputs.forEach(input => {
        input.addEventListener('input', function(e) {
            // You can add custom filtering logic here if needed
        });
    });
}

// Call on page load
document.addEventListener('DOMContentLoaded', loadCardNames);
```

---

## Future Enhancements (Not in Phase 1)

1. **View Readings Page**
   - Display all saved readings
   - Filter by date range
   - Search by card name

2. **Card Frequency Tracking**
   - Count how many times each card appears
   - Display statistics (most common cards, reversed vs upright)

3. **Edit/Delete Readings**
   - Ability to modify existing readings
   - Delete readings

4. **Export Functionality**
   - Export to CSV
   - Export to JSON
   - Export to Markdown (for journal)

5. **Spread Templates**
   - Pre-defined spread positions (Theme/Lesson/Focus, Past/Present/Future, etc.)

---

## Dependencies

### `requirements.txt`
```
Flask==3.0.0
```

---

## Notes

- **Text File Format:** Using JSONL (JSON Lines) format allows easy appending without loading entire file
- **ID Generation:** Simple increment based on existing readings
- **Date Handling:** Use Python's `datetime` for current date, store as string
- **Checkbox Handling:** In HTML forms, checkboxes only submit if checked. Use JavaScript or server-side logic to handle "false" values for unchecked boxes
- **Autocomplete:** Using HTML5 `<datalist>` provides native browser autocomplete. For more advanced features (like fuzzy matching), consider a lightweight library like Awesomplete or build a custom solution
- **Card Names File:** `tarot_cards.json` contains all 78 standard tarot cards (22 Major Arcana + 56 Minor Arcana). The `all_cards` array provides a flat list perfect for autocomplete

---

## Next Steps

1. Review and approve this plan
2. Create project structure
3. Implement Flask app skeleton
4. Build HTML form
5. Add JavaScript for toggle functionality
6. Implement backend save logic
7. Test and refine

