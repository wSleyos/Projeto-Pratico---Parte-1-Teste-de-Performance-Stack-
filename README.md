import React, { useRef } from 'react';
import { View, Text, StyleSheet, Button, Animated } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

const Stack = createNativeStackNavigator();

function TelaAnimacao() {
  const fadeAnim = useRef(new Animated.Value(0)).current;
  const translateYAnim = useRef(new Animated.Value(50)).current;

  const animar = () => {
    Animated.parallel([
      Animated.timing(fadeAnim, {
        toValue: 1,
        duration: 1000,
        useNativeDriver: true,
      }),
      Animated.timing(translateYAnim, {
        toValue: 0,
        duration: 1000,
        useNativeDriver: true,
      }),
    ]).start();
  };

  const resetar = () => {
    fadeAnim.setValue(0);
    translateYAnim.setValue(50);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Animação com Fade + Subida 🚀</Text>

      <Animated.View
        style={[
          styles.card,
          {
            opacity: fadeAnim,
            transform: [{ translateY: translateYAnim }],
          },
        ]}
      >
        <Text style={styles.cardTitulo}>Olá! Eu apareci ✨</Text>
        <Text style={styles.cardTexto}>
          Esse elemento sobe enquanto aparece na tela.
        </Text>
      </Animated.View>

      <View style={styles.botoes}>
        <Button title="Animar" onPress={animar} />
      </View>

      <View style={styles.botoes}>
        <Button title="Resetar" onPress={resetar} color="red" />
      </View>
    </View>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="TelaAnimacao"
          component={TelaAnimacao}
          options={{ title: 'Animação' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f2f2f2',
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  titulo: {
    fontSize: 26,
    fontWeight: 'bold',
    marginBottom: 30,
    textAlign: 'center',
  },
  card: {
    width: '100%',
    backgroundColor: '#fff',
    padding: 25,
    borderRadius: 16,
    elevation: 5,
    marginBottom: 30,
  },
  cardTitulo: {
    fontSize: 22,
    fontWeight: 'bold',
    marginBottom: 10,
    color: '#222',
  },
  cardTexto: {
    fontSize: 16,
    color: '#555',
    lineHeight: 22,
  },
  botoes: {
    width: '100%',
    marginBottom: 15,
  },
});
