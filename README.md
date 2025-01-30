// App.js (Main Component)
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';
import ProfileScreen from './screens/ProfileScreen';
import MatchesScreen from './screens/MatchesScreen';
import ChatScreen from './screens/ChatScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator
        screenOptions={{
          headerStyle: {
            backgroundColor: '#FFD700',
          },
          headerTintColor: '#2F2F2F',
          headerTitleStyle: {
            fontFamily: 'Cairo-Bold',
          }
        }}
      >
        <Stack.Screen name="Home" component={HomeScreen} 
          options={{ title: 'فدفد - FadFad' }} />
        <Stack.Screen name="Profile" component={ProfileScreen} 
          options={{ title: 'الملف الشخصي' }} />
        <Stack.Screen name="Matches" component={MatchesScreen} 
          options={{ title: 'المطابقات' }} />
        <Stack.Screen name="Chat" component={ChatScreen} 
          options={{ title: 'الدردشة' }} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
// components/ProfileCard.js
import React from 'react';
import { View, Text, Image, StyleSheet } from 'react-native';

const ProfileCard = ({ user }) => {
  return (
    <View style={styles.card}>
      <Image source={{ uri: user.photo }} style={styles.image} />
      <View style={styles.infoContainer}>
        <Text style={styles.name}>{user.name}، {user.age}</Text>
        <Text style={styles.location}>{user.location}</Text>
        <Text style={styles.bio}>{user.bio}</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#FFF',
    borderRadius: 15,
    margin: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.2,
    elevation: 3,
  },
  image: {
    width: '100%',
    height: 300,
    borderTopLeftRadius: 15,
    borderTopRightRadius: 15,
  },
  infoContainer: {
    padding: 15,
    alignItems: 'flex-end',
  },
  name: {
    fontFamily: 'Cairo-SemiBold',
    fontSize: 24,
    color: '#2F2F2F',
  },
  location: {
    fontFamily: 'Cairo-Regular',
    fontSize: 16,
    color: '#666',
  },
  bio: {
    fontFamily: 'Cairo-Light',
    fontSize: 14,
    color: '#444',
    marginTop: 10,
    textAlign: 'right',
  },
});

export default ProfileCard;
// screens/HomeScreen.js
import React, { useState } from 'react';
import { View, StyleSheet } from 'react-native';
import ProfileCard from '../components/ProfileCard';
import CustomButton from '../components/CustomButton';

const HomeScreen = ({ navigation }) => {
  const [currentProfile, setCurrentProfile] = useState({
    id: 1,
    name: 'ليلى',
    age: 26,
    location: 'دبي، الإمارات',
    bio: 'أحب السفر واكتشاف الثقافات الجديدة',
    photo: 'https://example.com/photo1.jpg',
  });

  return (
    <View style={styles.container}>
      <ProfileCard user={currentProfile} />
      
      <View style={styles.buttonsContainer}>
        <CustomButton 
          icon="close" 
          color="#FF4444" 
          onPress={() => handleSwipe('left')} 
        />
        <CustomButton 
          icon="heart" 
          color="#4CAF50" 
          onPress={() => handleSwipe('right')} 
        />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#FFFBE6',
  },
  buttonsContainer: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    padding: 20,
  },
});

export default HomeScreen;
// components/CustomButton.js
import React from 'react';
import { TouchableOpacity, StyleSheet } from 'react-native';
import Icon from 'react-native-vector-icons/FontAwesome';

const CustomButton = ({ icon, color, onPress }) => {
  return (
    <TouchableOpacity 
      style={[styles.button, { backgroundColor: color }]}
      onPress={onPress}
    >
      <Icon name={icon} size={30} color="white" />
    </TouchableOpacity>
  );
};

const styles = StyleSheet.create({
  button: {
    width: 60,
    height: 60,
    borderRadius: 30,
    justifyContent: 'center',
    alignItems: 'center',
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.2,
    elevation: 3,
  },
});

export default CustomButton;
