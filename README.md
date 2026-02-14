#GREEN-BOX
'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart'; // For WebView bot

class TourismHome extends StatefulWidget {
  @override
  _TourismHomeState createState() => _TourismHomeState();
}

class _TourismHomeState extends State<TourismHome> {
  int _currentIndex = 0;
  final List<TabItem> tabs = [
    TabItem('Hotels', Icons.hotel),
    TabItem('Restaurants', Icons.restaurant),
    TabItem('Travels', Icons.flight),
    TabItem('Safaris', Icons.eco),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: IndexedStack(
        index: _currentIndex,
        children: tabs.map((tab) => TabScreen(tab.title)).toList(),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) => setState(() => _currentIndex = index),
        items: tabs.map((tab) => BottomNavigationBarItem(
          icon: Icon(tab.icon), label: tab.title,
        )).toList(),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => Navigator.push(
          context,
          MaterialPageRoute(builder: (_) => ChatbotScreen()),
        ),
        child: Icon(Icons.chat),
        tooltip: 'Chat for Bookings',
      ),
    );
  }
}

class TabItem {
  final String title;
  final IconData icon;
  TabItem(this.title, this.icon);
}

class TabScreen extends StatelessWidget {
  final String title;
  TabScreen(this.title);
  @override
  Widget build(BuildContext context) {
    return Center(child: Text('$title Listings - Add your listings, maps, bookings here'));
  }
}

class ChatbotScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Booking Assistant')),
      body: WebView(
        initialUrl: 'https://your-chatbot-url.com?for=tourism', // e.g., Kommunicate/Thinkstack
        javascriptMode: JavascriptMode.unrestricted,
      ),
    );
  }
}
