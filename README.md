npm install -g expo-cli
expo init app-vente
npx expo startcd app-vente
https://wa.me/+25377372394?text=Commande:%0A${encodeURIComponent(message)
import React, { useState } from 'react';
import { View, Text, FlatList, Button, Image, StyleSheet } from 'react-native';
import * as Linking from 'expo-linking';

const produits = [
  { id: '1', nom: 'Chaussures sport', prix: 20000, image: 'https://via.placeholder.com/150' },
  { id: '2', nom: 'Montre connectée', prix: 35000, image: 'https://via.placeholder.com/150' },
];

export default function App() {
  const [panier, setPanier] = useState([]);

  const ajouterAuPanier = (produit) => {
    setPanier([...panier, produit]);
  };

  const envoyerCommandeWhatsApp = () => {
    const message = panier.map(p => `${p.nom} - ${p.prix} DJF`).join('\n');
    const url = `https://wa.me/TON_NUMERO?text=Commande:%0A${encodeURIComponent(message)}`;
    Linking.openURL(url);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Boutique en ligne</Text>
      <FlatList
        data={produits}
        keyExtractor={item => item.id}
        renderItem={({ item }) => (
          <View style={styles.card}>
            <Image source={{ uri: item.image }} style={styles.image} />
            <Text>{item.nom}</Text>
            <Text>{item.prix} DJF</Text>
            <Button title="Ajouter" onPress={() => ajouterAuPanier(item)} />
          </View>
        )}
      />
      <Button title="Commander via WhatsApp" onPress={envoyerCommandeWhatsApp} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20 },
  title: { fontSize: 24, fontWeight: 'bold', marginBottom: 20 },
  card: { marginBottom: 15, padding: 10, backgroundColor: '#eee' },
  image: { width: 150, height: 150, marginBottom: 10 }
