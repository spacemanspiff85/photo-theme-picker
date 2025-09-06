# Monthly Photo Theme Picker

A fun, interactive web application for photo clubs to randomly select monthly photography themes with smart weighting to encourage variety while avoiding recent repeats.

## Features

### Core Functionality
- **Random Theme Generation**: Generates 3 random themes from a database of 130+ photography themes
- **Smart Weighting Algorithm**: Recently used themes are less likely (but not impossible) to appear
  - Themes used within 3 months: 10% selection weight
  - Themes used within 6 months: 20% selection weight
  - Themes never used or >6 months ago: 100% selection weight
- **July Tradition**: Automatically suggests "Americana" for July themes
- **Custom Theme Option**: Add a 4th custom theme option for voting
- **Shuffle Feature**: Not happy with the selection? Keep shuffling for new themes

### Theme Categories
The app includes 130+ themes organized into 8 categories:
1. **The Human Environment** (41 themes) - streetscapes, architecture, people, etc.
2. **Seasonal** (11 themes) - holidays and seasons
3. **Nature** (19 themes) - landscapes, wildlife, weather
4. **Time of Day** (6 themes) - sunset, sunrise, blue hour, etc.
5. **Emotions** (11 themes) - joy, peace, love, etc.
6. **Form & Techniques** (35 themes) - patterns, shadows, macro, etc.
7. **Colors** (10 themes) - red, blue, green, etc.
8. **Club Made** (dynamic) - custom themes created by your photo club

### History Management
- **Track Used Themes**: Keep a complete history of which themes were used each month
- **Edit History**: Add, edit, or delete historical entries
- **Backfill Missing Months**: Fill in gaps in your historical record
- **Automatic Club Made Themes**: Custom themes from history automatically become available for future selection

## How to Use

### Getting Started
1. Open `index.html` in any modern web browser
2. The app will automatically load with any previously saved history

### Generating Themes
1. Click the **"Generate 3 Themes"** button
2. Three random themes will appear, each labeled with its category
3. Optionally enter a 4th custom theme in the input field
4. If you don't like the selection, click **"Shuffle Again"** for new themes
5. Keep shuffling until you find themes your group likes!

### Recording the Winner
1. After your group votes, click **"Mark Winner as Used"**
2. Select the winning theme from the dropdown
3. Confirm the month and year (defaults to current month)
4. Click **Save** to record it in history

### Managing History
- **View History**: The last 12 months are displayed in the history table
- **Edit Entry**: Click the "Edit" button next to any month
- **Delete Entry**: Click the "Delete" button to remove an entry
- **Add Historical Entry**: Click "+ Add Historical Entry" to backfill missing months

### Club Made Themes
When you add a custom theme to history that isn't in the standard database, it automatically:
- Gets added to the "Club Made" category
- Becomes available for future random selection
- Appears with a special "Club Made" badge when selected

## Technical Details

### Data Storage
- All data is stored locally in your browser using localStorage
- No server or internet connection required after initial load
- Data persists between sessions

### Browser Compatibility
- Works on all modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile-responsive design for phones and tablets
- No installation required - just open and use

## Pre-loaded History

The app comes with the following historical themes already loaded:
- July 2023: Americana
- March 2024: Spring has sprung
- May 2024: Shadows
- June 2024: Summer is here
- July 2024: Americana
- May 2025: The extraordinary in the ordinary
- June 2025: Americana
- July 2025: Simple Joy
- August 2025: Weather

## Tips for Photo Clubs

1. **Monthly Rotation**: Rotate who selects themes each month to keep it fair
2. **Vote Quickly**: Generate themes at the start of your meeting and vote immediately
3. **Document Results**: Always mark the winner to maintain accurate history
4. **Embrace Variety**: The weighting system encourages exploring new themes while occasionally revisiting favorites
5. **Custom Creativity**: Use the custom theme option to propose timely or location-specific themes

## Troubleshooting

**Themes not saving?**
- Check that your browser allows localStorage
- Try a different browser if issues persist

**Want to reset everything?**
- Open browser developer tools (F12)
- Go to Console
- Type: `localStorage.clear()`
- Refresh the page

**Missing the July Americana tradition?**
- The app only auto-suggests Americana when generating themes in July
- You can still manually add "Americana" for any July in history

## Future Enhancements (Not Yet Implemented)

Ideas for future versions:
- Photo gallery for each month's submissions
- Built-in voting mechanism
- AI-powered theme suggestions
- Export/import history data
- Theme difficulty ratings
- Seasonal theme suggestions

## Credits

Created for photo clubs everywhere who love a good monthly challenge!

---

*Happy shooting! May your themes be inspiring and your photos be sharp!* 📸