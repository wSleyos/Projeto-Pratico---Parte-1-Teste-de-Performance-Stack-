import React, { useState, memo } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

const Stack = createNativeStackNavigator();

// Componente que renderiza sempre
function FilhoLento() {
  console.log('FilhoLento renderizou');

  return (
    <View style={[styles.card, styles.cardLento]}>
      <Text style={styles.tituloCard}>Filho Lento 🐢</Text>
      <Text style={styles.textoCard}>
        Esse componente renderiza toda vez que o pai atualiza.
      </Text>
    </View>
  );
}

// Componente otimizado com React.memo
const FilhoRapido = memo(function FilhoRapido() {
  console.log('FilhoRapido renderizou');

  return (
    <View style={[styles.card, styles.cardRapido]}>
      <Text style={styles.tituloCard}>Filho Rápido ⚡</Text>
      <Text style={styles.textoCard}>
        Esse componente renderiza apenas uma vez.
      </Text>
    </View>
  );
});

// Tela principal
function TelaPerformance() {
  const [contador, setContador] = useState(0);

  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Teste de Performance 🚀</Text>
      <Text style={styles.contador}>Contador do Pai: {contador}</Text>

      <Button
        title="Incrementar Pai"
        onPress={() => setContador(contador + 1)}
      />

      <FilhoLento />
      <FilhoRapido />
    </View>
  );
}

// App principal
export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="TelaPerformance"
          component={TelaPerformance}
          options={{ title: 'Performance' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

// Estilos
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f2f2f2',
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  titulo: {
    fontSize: 28,
    fontWeight: 'bold',
    marginBottom: 15,
    textAlign: 'center',
  },
  contador: {
    fontSize: 22,
    marginBottom: 20,
    color: '#333',
  },
  card: {
    width: '100%',
    backgroundColor: '#fff',
    padding: 20,
    marginTop: 20,
    borderRadius: 16,
    elevation: 4,
  },
  cardLento: {
    borderLeftWidth: 6,
    borderLeftColor: 'red',
  },
  cardRapido: {
    borderLeftWidth: 6,
    borderLeftColor: 'green',
  },
  tituloCard: {
    fontSize: 22,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  textoCard: {
    fontSize: 16,
    color: '#444',
    lineHeight: 22,
  },
});
