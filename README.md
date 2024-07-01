# Tugas-Laporan
pemograman mobile

App.js
import React from 'react';
import {Text, View, StyleSheet, Button} from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import Home from './components/home';
import About from './components/about';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="About" component={About} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

About.js
import React from 'react';
import { View, Text, StyleSheet, Button, Image } from 'react-native';

const About = ({ route, navigation }) => {
  const { contact } = route.params;

  return (
    <View style={styles.container}>
      <Image source={contact.gambar} style={styles.img} />
      <Text style={styles.title}>{contact.judul}</Text>
      <Text style={styles.telpon}>Telpon: {contact.telpon}</Text>
      <Text style={styles.tanggalLahir}>Tanggal Lahir: {contact.tanggalLahir}</Text>
      <Text style={styles.catatan}>Catatan: {contact.catatan}</Text>
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#fff',
  },
  img: {
    width: 100,
    height: 100,
    marginBottom: 20,
    borderRadius: 50, // rounded image
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
  },
  telpon: {
    fontSize: 18,
    color: '#3498db',
    marginBottom: 10,
  },
  tanggalLahir: {
    fontSize: 20,
    marginBottom: 10,
  },
  catatan: {
    fontSize: 20,
    marginBottom: 10,
  },
});

export default About;

Contact.js
import React from 'react';
import { View, Text, Image, StyleSheet, TouchableOpacity } from 'react-native';
import { useNavigation } from '@react-navigation/native';

export default function Contact(props) {
  const navigation = useNavigation();

  const handlePress = () => {
    navigation.navigate('About', { contact: props });
  };

  return (
    <TouchableOpacity onPress={handlePress} style={styles.container}>
      <Image source={props.gambar} style={styles.img} />
      <View style={styles.teks}>
        <Text style={styles.title}>{props.judul}</Text>
        <Text style={styles.telp}>{props.telpon}</Text>
      </View>
      <View style={styles.buttonContainer}>
        <TouchableOpacity onPress={handlePress} style={styles.button}>
          <Text style={styles.buttonText}>Detail</Text>
        </TouchableOpacity>
      </View>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  container: {
    height: 80,
    flexDirection: 'row',
    alignItems: 'center',
    borderBottomWidth: 1,
    borderColor: 'blue',
    paddingHorizontal: 10,
  },
  img: {
    margin: 15,
    width: 50,
    height: 50,
    borderRadius:25,
  },
  teks: {
    flex: 1,
  },
  title: {
    fontWeight: 'bold',
    fontSize: 16,
  },
  telp: {
    fontSize: 14,
    color: '#3498db',
  },
  buttonContainer: {
    justifyContent: 'center',
    alignItems: 'center',
  },
  button: {
    backgroundColor: '#3498db',
    padding: 5,
    borderRadius: 5,
  },
  buttonText: {
    color: '#fff',
    fontSize: 14,
  },
});

Home.js
import React from 'react';
import { View, Text, StyleSheet, FlatList, TouchableOpacity } from 'react-native';
import Contact from './contact';

const contacts = [
  { id: '1', judul: 'hilman', telpon: '081888310104', gambar: require('../assets/hilman.jpg,jpg'), tanggalLahir: '31 January 2004', catatan: 'suami' },
  { id: '2', judul: 'jaki', telpon: '088818010431', gambar: require('../assets/jaki.jpg.jpg'), tanggalLahir: '2 Desember 2003', catatan:'suami'},
  { id: '3', judul: 'Leonardo', telpon: '083101188804', gambar: require('../assets/Leonardo.jpg'), tanggalLahir: '1 January 2004', catatan: 'suami' },
  { id: '4', judul: 'zaldi', telpon: '081831880401', gambar: require('../assets/zaldi.jpg'), tanggalLahir: '1 Januar2004', catatan: 'suami' },
  { id: '5', judul: 'fauzan', telpon: '080131180488', gambar: require('../assets/fauzan.jpg'), tanggalLahir: '2 January 2004', catatan: 'suami' },
  { id: '6', judul: 'firhan', telpon: '0818043100188', gambar: require('../assets/firhan.jpeg'), tanggalLahir: '2 January 2004', catatan: 'suami' },
];

const Home = ({ navigation }) => {
  const renderContactItem = ({ item }) => (
    <TouchableOpacity
      style={styles.contactContainer}
      onPress={() => navigation.navigate('About', { contact: item })}
    >
      <Contact
        judul={item.judul}
        telpon={item.telpon}
        gambar={item.gambar}
      />
    </TouchableOpacity>
  );

  return (
    <View style={styles.container}>
      <FlatList
        data={contacts}
        keyExtractor={item => item.id}
        renderItem={renderContactItem}
        ListHeaderComponent={<Text style={styles.header}>Daftar Teman</Text>}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  header: {
    fontSize: 20,
    fontWeight: 'bold',
    textAlign: 'center',
    marginVertical: 10
  },
  contactContainer: {
    paddingHorizontal: 10,
    marginBottom: 10,
  },
});

export default Home;

